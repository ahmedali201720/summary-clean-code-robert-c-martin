# Chapter 1 — Clean Code

> *Clean Code* by Robert C. Martin ("Uncle Bob"). Principles faithful to the original; examples in JS/TS/React.
> **Nav:** [Index](00-index.md) · Next → [02 Meaningful Names](02-meaningful-names.md)

*What "clean" means, why messes cost you, and the one rule that keeps a codebase alive.*

---

## The core idea

Code is read far more often than it is written — the reading-to-writing ratio is well over **10:1**. Every time you write a line, you're reading the surrounding code to decide what to write. So making code easy to read is what makes it easy to *write* — and cheap to change.

**There will always be code.** Higher-level tools and abstractions don't remove the need to specify behavior precisely; they just raise the level at which we do it. The question is never *whether* we write code, but whether we write it **well**.

## The cost of a mess

Bad code slows every future edit. Productivity drops as the mess grows, until it approaches zero and the team demands a **grand redesign in the sky** — a full rewrite that rarely goes better than the original (and now you're maintaining two systems). The mess is a debt with compounding interest.

## What is clean code?

Martin collects definitions from famous programmers. The recurring themes:

- **Focused** — each piece does one thing well.
- **Readable** — reads like well-written prose; it's obvious, not surprising.
- **No duplication.**
- **Cared for** — it looks like someone was paying attention.

> Clean code always looks like it was written by someone who cares. There is nothing obvious you can do to make it better.

We are **authors**: we write for human readers. Code is communication first, instruction to the machine second.

## The Boy Scout Rule

The single most portable idea in the book:

> **Leave the code cleaner than you found it.**

You don't need a refactoring sprint. Rename one unclear variable, split one long function, delete one dead branch — per commit. Cleanup compounds.

```js
// before you touched the file
function calc(x, y, t) {
  return t === 1 ? x + y : t === 2 ? x - y : x * y;
}

// after — 30 seconds of care
const Op = { Add: 'add', Sub: 'sub', Mul: 'mul' };

function apply(a, b, op) {
  switch (op) {
    case Op.Add: return a + b;
    case Op.Sub: return a - b;
    case Op.Mul: return a * b;
  }
}
```

## Takeaway

You can't make a system clean in one heroic pass. You keep it clean the way you keep a kitchen clean — continuously, in small acts, every time you're in there.
