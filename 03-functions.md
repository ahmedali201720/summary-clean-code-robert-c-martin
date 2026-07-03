# Chapter 3 — Functions

> *Clean Code* by Robert C. Martin ("Uncle Bob"). Principles faithful to the original; examples in JS/TS/React.
> **Nav:** ← [02 Meaningful Names](02-meaningful-names.md) · [Index](00-index.md) · Next → [04 Comments](04-comments.md)

*The chapter that changes how you write. Small, one job, few arguments, no surprises.*

---

## The two rules of size

> The first rule of functions is that they should be **small**. The second rule is that they should be **smaller than that**.

Realistically: a handful of lines. Blocks inside `if`/`for`/`while` should be **one line** — usually a function call. That keeps a function to a single level of indentation and gives the called function a descriptive name.

## Do one thing

> Functions should do one thing. They should do it well. They should do it only.

The test: you can't extract another function from it with a name that isn't just a restatement of what it does. Everything in the function should sit at **one level of abstraction** — don't mix high-level policy with low-level string fiddling.

**The Stepdown Rule:** the code reads top-down like a narrative. Each function is followed by those at the next level down, so you read policy first and drill into detail only when you want it.

```ts
// smell: many things, mixed levels of abstraction
async function register(req) {
  const e = req.body.email;
  if (!/^\S+@\S+$/.test(e)) throw new Error('bad');
  const exists = await db.query('select 1 from users where email=$1', [e]);
  if (exists.rows.length) throw new Error('dup');
  const h = await bcrypt.hash(req.body.pw, 10);
  await db.query('insert into users...', [e, h]);
  await mailer.send(e, 'Welcome');
}

// clean: reads top-down as a story
async function register({ email, password }) {
  assertValidEmail(email);
  await assertEmailIsFree(email);
  const user = await createUser(email, password);
  await sendWelcome(user);
  return user;
}
// each helper lives one level below — policy first, details on demand
```

## Switch statements

A `switch` inherently does N things. Tolerate it once — buried low, behind an abstraction, used to create polymorphic objects — but don't repeat the same switch across the codebase. Prefer polymorphism (see Ch. 17, G23).

## Function arguments

- **0 is ideal, 1–2 is fine, 3 is hard, more should be avoided.** Each argument is another thing the reader must hold in mind, and another axis to test.
- **Flag arguments are a smell.** `render(true)` tells the reader nothing and proves the function does two things. Split it, or pass an options object.
- **Wrap related args in an object.** `makeCircle(x, y, radius)` → `makeCircle(center, radius)`.

```js
// smell: flag argument
function renderPage(page, isSuite) {
  if (isSuite) { /* ... */ } else { /* ... */ }
}
renderPage(p, true);  // true what?

// clean: split by intent
function renderPageForSuite(page) { /* ... */ }
function renderPageForData(page)  { /* ... */ }
renderPageForSuite(p);
```

## Have no side effects · Command–Query Separation

- **No side effects.** A function named `checkPassword` must not secretly also initialize a session — hidden side effects create temporal coupling.
- **Command–Query Separation.** A function should *either do something or answer something, but not both*. `set(...)` changes state (command) **or** `get(...)` returns a value (query) — never a `set()` that returns a boolean you have to decode.
- **Output arguments are a smell.** Prefer changing the state of the owning object, or returning a new value, over mutating an argument.

## Error handling & DRY

- **Prefer exceptions to returning error codes** — error codes force the caller to check and nest immediately (full treatment in Ch. 7).
- **Extract try/catch blocks** into their own function so error handling *is* that function's one thing.
- **Don't Repeat Yourself.** Duplication is the root of much evil; most rules in this chapter are partly an attack on it.

## How do you write functions like this?

You don't — not at first. You get it working, ugly, with tests. Then you **refactor**: split functions, rename, remove duplication, all while the tests stay green.

## Takeaway

Functions are the verbs of your system. Master this one chapter — small, single-purpose, honestly named, side-effect-free — and most other rules follow.
