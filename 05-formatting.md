# Chapter 5 — Formatting

> *Clean Code* by Robert C. Martin ("Uncle Bob"). Principles faithful to the original; examples in JS/TS/React.
> **Nav:** ← [04 Comments](04-comments.md) · [Index](00-index.md) · Next → [06 Objects & Data Structures](06-objects-and-data-structures.md)

*Formatting is communication, and communication is the professional's first order of business.*

---

## The core idea

Formatting isn't cosmetic — it signals care and directly aids reading. A reader's first impression of your professionalism is how the code *looks* before they understand a line of it.

## Vertical formatting

- **Openness between concepts.** Blank lines separate distinct thoughts; tightly related lines stay together with no gaps.
- **The newspaper metaphor.** A file reads top-down: the name and high-level concepts are at the top (the headline), details descend as you read.
- **Vertical distance.** Related things belong near each other. A calling function sits just above the one it calls; variables are declared close to where they're used; related functions stay together.
- **File length.** Most well-formed files are a few hundred lines, not thousands. Small files are easier to understand.

## Horizontal formatting

- **Keep lines short.** You should never have to scroll right. Short lines force clearer expressions.
- **Horizontal openness** groups related tokens and separates unrelated ones.
- **Indentation** shows the hierarchy of scope — don't collapse it even for one-line blocks.

## Team rules beat personal taste

A codebase should look like it was written by a **single mind**. The team agrees on one style and applies it everywhere; individual preference yields to consistency.

## Takeaway

Uncle Bob wrote this before the modern JS tooling existed, but it maps perfectly:

- **Prettier** — automatic formatting, so nobody argues about spaces or line length.
- **ESLint** — enforces the team's rules (unused vars, import order, etc.).
- Run both in a **pre-commit hook** and in **CI**.

That *is* his "one team style, applied automatically" — now free and instant.
