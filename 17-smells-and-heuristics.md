# Chapter 17 — Smells & Heuristics

> *Clean Code* by Robert C. Martin ("Uncle Bob"). Principles faithful to the original; examples in JS/TS/React.
> **Nav:** ← [16 Refactoring SerialDate](16-refactoring-serialdate.md) · [Index](00-index.md)

*The payoff chapter: a catalog of ~66 code smells and their fixes, grouped by category. Your review checklist.*

---

This is the whole book distilled into a reference you scan during code review. Each item has a code: **C** = Comments, **E** = Environment, **F** = Functions, **G** = General, **J** = Java (language-specific), **N** = Names, **T** = Tests. The most valuable, framework-agnostic ones:

## Comments (C)

| Code | Smell | Fix |
|---|---|---|
| C1 | Inappropriate information | Keep change history and metadata out of comments — that's for other tools. |
| C2 | Redundant comment | If it just restates the code, delete it. |
| C3 | Poorly written comment | If you write one, make it worth reading — brief, correct, clear. |
| C5 | Commented-out code | Delete on sight; it accumulates and no one dares remove it. |

## Functions (F)

| Code | Smell | Fix |
|---|---|---|
| F1 | Too many arguments | Zero–two ideal; wrap related args in an object. |
| F2 | Output arguments | A function should change its own object's state or return a value — not mutate a passed-in arg. |
| F3 | Flag arguments | A boolean param proves the function does two things — split it. |
| F4 | Dead function | Never called? Delete it. Source control remembers. |

## General (G) — the largest group

| Code | Smell | Fix |
|---|---|---|
| G5 | Duplication | The #1 enemy. Every repeated block is a missed abstraction — DRY it. |
| G6 | Code at wrong level of abstraction | Don't mix high-level concepts and low-level detail in one place. |
| G8 | Too much information | Keep interfaces small and tight; hide everything you can. |
| G9 | Dead code | Remove unreachable branches and unused code — it misleads readers. |
| G11 | Inconsistency | Do similar things the same way throughout the codebase. |
| G14 | Feature envy | A method that reaches into another object's data belongs on that object. |
| G15 | Magic numbers/strings | Replace literals like `86400` with named constants (`SECONDS_PER_DAY`). |
| G19 | Use explanatory variables | Break a complex expression into well-named intermediate values. |
| G20 | Function names say what they do | The name should tell the caller everything, so they needn't read the body. |
| G23 | Prefer polymorphism to if/else & switch | Replace repeated type-switches with polymorphic types. |
| G25 | Replace magic numbers with named constants | (Restated — it matters that much.) |
| G28 | Encapsulate conditionals | `if (shouldBeDeleted(timer))` beats a raw boolean expression. |
| G30 | Functions should do one thing | The heartbeat of Ch. 3, restated as a review rule. |
| G31 | Hidden temporal couplings | Make required call order explicit (e.g. return a value the next call needs). |
| G34 | Functions should descend one level of abstraction | Keep each function at a single conceptual level. |
| G36 | Avoid transitive navigation | Don't reach through `a.b.c.d` (Law of Demeter — see Ch. 6). |

## Names (N)

| Code | Smell | Fix |
|---|---|---|
| N1 | Non-descriptive / unclear name | Choose names that reveal intent; rename freely. |
| N2 | Name at wrong abstraction level | Name for the concept, not the current implementation. |
| N4 | Unambiguous / scoped names | A name should be as long as its scope is large. |
| N7 | Names describe side effects | If a function does more than its name implies, rename or split it. |

## Tests (T)

| Code | Smell | Fix |
|---|---|---|
| T1 | Insufficient tests | Test everything that could plausibly break, not just the happy path. |
| T2 | Use a coverage tool | Let it show you the gaps. |
| T3 | Don't skip trivial tests | They're easy and their documentary value exceeds their cost. |
| T5 | Test boundary conditions | Bugs cluster at the edges. |
| T6 | Exhaustively test near bugs | One bug found means more are nearby — look. |
| T9 | Tests should be fast | Slow tests get skipped; skipped tests stop protecting you. |

## Takeaway

Keep this chapter open during pull-request reviews. The smells give your team a shared vocabulary — "this is feature envy," "G15, magic number," "F3, flag argument" — that makes reviews faster, more objective, and less personal.
