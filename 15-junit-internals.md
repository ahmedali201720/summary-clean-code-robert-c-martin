# Chapter 15 — JUnit Internals

> *Clean Code* by Robert C. Martin ("Uncle Bob"). Principles faithful to the original; examples in JS/TS/React.
> **Nav:** ← [14 Successive Refinement](14-successive-refinement.md) · [Index](00-index.md) · Next → [16 Refactoring SerialDate](16-refactoring-serialdate.md)

*Even code by masters can be made cleaner. A respectful refactor of a beloved library.*

---

## What the chapter does

Martin takes real source from **JUnit** itself — the `ComparisonCompactor`, the code that produces those helpful string-difference messages when an assertion fails — and cleans it up. The original is written by respected engineers and is already good, yet he still finds improvements.

## The lesson

- **No code is above the Boy Scout Rule.** However good the author, there's usually clarity you can add for the next reader. Improvement is continuous and humble — not a verdict on the original author.

- **The cleanup is a series of tiny, obvious improvements,** not a dramatic rewrite:
  - better, more precise **names**;
  - **splitting** functions so each does one thing;
  - removing **negatives** and awkward conditionals that force the reader to think backwards;
  - reducing **temporal coupling** and hidden state;
  - all while the JUnit tests stay **green**.

- **Critique with respect.** Reviewing and refactoring someone's code isn't disparagement; it's the normal, professional act of leaving shared code a little better.

## Takeaway

"Good enough" code still has readability you can add. Treat every file you open — even a well-crafted one — as a chance to make the next reader's job easier, in small verified steps.
