# Chapter 12 — Emergence

> *Clean Code* by Robert C. Martin ("Uncle Bob"). Principles faithful to the original; examples in JS/TS/React.
> **Nav:** ← [11 Systems](11-systems.md) · [Index](00-index.md) · Next → [13 Concurrency](13-concurrency.md)

*Good design isn't drawn up front — it emerges by following four rules, in order.*

---

## Kent Beck's four rules of Simple Design

A design is "simple" — and good structure (SRP, DIP, low coupling, high cohesion) emerges on its own — if it follows these four rules, **listed in order of importance**:

### 1. Runs all the tests

A design you can't verify is worthless. And making a system testable *drives* good design: to test a class in isolation you're pushed toward small, single-purpose units with low coupling (dependency injection, interfaces, abstractions). Testability and clean design reinforce each other.

### 2. Contains no duplication

With tests as a safety net, you can refactor relentlessly. **Duplication is the primary enemy** of a clean design — every repeated block is a missed abstraction. Remove it aggressively (see Ch. 17, G5).

### 3. Expresses the intent of the programmer

Code should clearly say what it does: good names, small functions and classes, and standard patterns readers recognize by name. The easier code is to read, the cheaper it is to maintain.

### 4. Minimizes the number of classes and methods

Keep the count low — but this rule is **last**. Don't over-fragment into dozens of tiny needless classes, and never sacrifice tests, deduplication, or expressiveness just to shrink the count.

> Rules 2–4 are essentially **refactoring**. Once you have tests (rule 1), you're free to clean up without fear of breaking anything.

## The engine

The practical loop that ties Ch. 9 (tests) to design:

**make it pass → remove duplication → make it expressive → keep it minimal → repeat**

Do this after every few lines. Good design isn't a diagram you draw once; it's the residue of applying these rules continuously.

## Takeaway

You don't need to architect everything up front. Write a failing test, make it pass, then clean under green — dedupe, clarify, minimize. Do that faithfully and the design that emerges will be better than one you could have planned.
