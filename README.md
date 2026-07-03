# Clean Code — Chapter-by-Chapter Summary

A developer's summary of **Clean Code: A Handbook of Agile Software Craftsmanship** by Robert C. Martin ("Uncle Bob"), split into one file per chapter. Principles are faithful to the original; the book's Java examples are re-cast in **JavaScript / TypeScript / React**.

**Core thesis:** code is read ~10× more than it's written, so optimize for reading. A mess accrues a "total cost of ownership" that slows every change until velocity approaches zero. Clean code is focused, readable, duplication-free, and looks like *someone cared*.

## Chapters

| # | Chapter | In one line |
|---|---|---|
| 01 | [Clean Code](01-clean-code.md) | What "clean" means and the Boy Scout Rule. |
| 02 | [Meaningful Names](02-meaningful-names.md) | The name is the comment you can't get wrong. |
| 03 | [Functions](03-functions.md) | Small, one thing, few args, no side effects. |
| 04 | [Comments](04-comments.md) | A comment is a failure to express yourself in code. |
| 05 | [Formatting](05-formatting.md) | Communication; in JS that's Prettier + ESLint. |
| 06 | [Objects & Data Structures](06-objects-and-data-structures.md) | Hide data (objects) vs expose data (DTOs); Law of Demeter. |
| 07 | [Error Handling](07-error-handling.md) | Throw, don't return codes; never return/pass null. |
| 08 | [Boundaries](08-boundaries.md) | Wrap third-party code behind your own seam. |
| 09 | [Unit Tests](09-unit-tests.md) | TDD, F.I.R.S.T, one concept per test, clean tests. |
| 10 | [Classes](10-classes.md) | Small, single responsibility, high cohesion. |
| 11 | [Systems](11-systems.md) | Separate construction from use; dependency injection. |
| 12 | [Emergence](12-emergence.md) | Four rules of simple design. |
| 13 | [Concurrency](13-concurrency.md) | Decouple what from when; no shared mutable state. |
| 14 | [Successive Refinement](14-successive-refinement.md) | Make it work, then clean it in small green steps. |
| 15 | [JUnit Internals](15-junit-internals.md) | Even great code is improvable; Boy Scout Rule. |
| 16 | [Refactoring SerialDate](16-refactoring-serialdate.md) | Cover with tests, then refactor fearlessly. |
| 17 | [Smells & Heuristics](17-smells-and-heuristics.md) | ~66-item review checklist, coded by category. |

## One-screen cheat sheet

| Area | Rules |
|---|---|
| **Names** | Reveal intent; nouns for classes, verbs for methods; one word/concept; length ∝ scope |
| **Functions** | Small→smaller; one thing, one abstraction level; ≤2 args; no flags; no side effects; command *or* query |
| **Comments** | Best comment = better code; delete commented-out code; explain intent/warnings only |
| **Errors** | Throw, don't return codes; never return/pass `null`; give exceptions context |
| **Classes/Systems** | One responsibility, high cohesion; depend on abstractions (DIP); separate construction from use (DI) |
| **Tests/Design** | F.I.R.S.T; one concept/test; pass→dedupe→express→minimize; Boy Scout Rule every commit |

*Read the book itself for the full worked case studies in Ch. 14–16.*
