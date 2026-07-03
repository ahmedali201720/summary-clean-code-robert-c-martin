# Chapter 4 — Comments

> *Clean Code* by Robert C. Martin ("Uncle Bob"). Principles faithful to the original; examples in JS/TS/React.
> **Nav:** ← [03 Functions](03-functions.md) · [Index](00-index.md) · Next → [05 Formatting](05-formatting.md)

*A comment is a failure to express yourself in code. Sometimes necessary — usually a smell.*

---

## The core idea

Comments don't compile, so they **rot**: the code changes and the comment quietly starts to lie. The best comment is the one you didn't have to write because the code says it.

> Don't comment bad code — rewrite it.

```js
// smell: comment compensating for unclear code
// Check if employee is eligible for full benefits
if (emp.flags & HOURLY && emp.age > 65) { /* ... */ }

// clean: the code says it itself
if (emp.isEligibleForFullBenefits()) { /* ... */ }
```

## Good comments (the short list)

- **Legal** — copyright / license headers.
- **Informative** — e.g. explaining what a gnarly regex matches.
- **Explanation of intent** — why you chose this approach.
- **Warning of consequences** — "this test takes 10 minutes, don't run casually."
- **TODO** — planned work, with the intent to actually do it.
- **Amplification** — flagging something that looks trivial but isn't.
- **Public API docs** — JSDoc/TSDoc on a published interface.

## Bad comments (the long list, in practice)

- **Redundant** — restates the code (`i++; // increment i`).
- **Mumbling** — a note to yourself no reader can decode.
- **Misleading** — subtly wrong, worse than none.
- **Mandated** — a comment on every function because a rule says so.
- **Journal comments** — change logs at the top of a file. That's version control's job.
- **Noise** — `/** The day of the month. */ private day;`
- **Position markers** and **closing-brace comments** — `} // end for`.
- **Attributions / bylines** — `// Added by Rick`. Git knows.
- **Commented-out code** — **delete it.** It accumulates like sludge; others fear to remove it because "it might be important."

## Takeaway

Before writing a comment, try to make it unnecessary — usually with a better name or an extracted function. When you genuinely can't, keep the comment short, right next to the code, and true.
