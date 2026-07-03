# Chapter 7 — Error Handling

> *Clean Code* by Robert C. Martin ("Uncle Bob"). Principles faithful to the original; examples in JS/TS/React.
> **Nav:** ← [06 Objects & Data Structures](06-objects-and-data-structures.md) · [Index](00-index.md) · Next → [08 Boundaries](08-boundaries.md)

*Error handling is important, but if it obscures logic, it's wrong.*

---

## The rules

- **Use exceptions, not return codes.** Return codes clutter the caller with immediate checks, tangle the happy path, and get silently forgotten.
- **Write your `try` first.** A `try/catch/finally` defines a scope, like a transaction. Build the happy path inside it, then the failure path. Then **extract the body** into its own function so error handling *is* the one thing that outer function does.
- **Provide context with exceptions.** The message should say what you were attempting and why it failed — enough to diagnose from a log.
- **Define exception classes around the caller's needs**, not around their source. Wrapping a third-party library's many error types in one of your own often simplifies callers dramatically.
- **Don't return `null`.** It pushes a null-check onto every caller, and one missed check is a crash. Return an empty array, a sensible default, or throw.
- **Don't pass `null`** into methods either — it invites the same failure from the inside.

```ts
// smell: error codes + null, logic buried in checks
function getUser(id) {
  const u = repo.find(id);
  if (!u) return null;
  return u;
}
const u = getUser(id);
if (u !== null) {            // every caller must remember
  if (u.roles !== null) { /* ... */ }  // ...and again
}

// clean: throw, or return a safe default
function getUser(id) {
  const u = repo.find(id);
  if (!u) throw new NotFoundError(`user ${id} not found`);
  return { ...u, roles: u.roles ?? [] };
}

try {
  const u = getUser(id);
  render(u);
} catch (e) {
  showError(e.message);
}
```

## In TypeScript

Two clean options, depending on whether the failure is *expected*:

- **Expected failures** (validation, not-found): model them in the type with a `Result` union, so the compiler forces callers to handle both branches.

  ```ts
  type Result<T, E> = { ok: true; value: T } | { ok: false; error: E };
  ```

- **Truly exceptional failures** (out of memory, programmer bug): `throw`.

Either way, keep the happy path readable and stop callers from drowning in null checks.

## Takeaway

Separate error handling from logic. Exceptions with good messages, no `null` in or out, and one function whose only job is the try/catch — that's clean error handling.
