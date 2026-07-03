# Chapter 10 — Classes

> *Clean Code* by Robert C. Martin ("Uncle Bob"). Principles faithful to the original; examples in JS/TS/React.
> **Nav:** ← [09 Unit Tests](09-unit-tests.md) · [Index](00-index.md) · Next → [11 Systems](11-systems.md)

*Classes should be small. Then smaller. Size is measured in responsibilities, not lines.*

---

## Classes should be small

The first rule is that they should be small; the second is that they should be **smaller than that**. But for classes, "small" is measured in **responsibilities**, not lines. A class name should describe its single responsibility; if you can only name it with vague words like `Manager`, `Processor`, or `Super`, or you need "and," it's doing too much.

## The Single Responsibility Principle (SRP)

> A class should have one, and only one, reason to change.

Many small, single-purpose classes beat a few large multipurpose ones. This isn't more complexity — it's the *same* complexity, organized so you can find and change one thing at a time. A large class with 70 methods is harder to navigate than 10 focused classes.

```ts
// smell: one class, many reasons to change
class UserService {
  validate() {}
  saveToDb() {}
  sendEmail() {}
  renderProfileHtml() {}
  exportCsv() {}
}
// DB, mail, view, and export concerns all tangled together

// clean: each has one job
class UserValidator  { validate(u) {} }
class UserRepository { save(u) {} }
class WelcomeMailer  { send(u) {} }
// compose them; each is tiny and independently testable
```

## Cohesion

A class is **cohesive** when most of its methods use most of its instance fields. High cohesion means the methods and data belong together. When you notice cohesion dropping — a few methods use one subset of fields, others use a different subset — that's the signal to **split** the class into smaller, cohesive ones.

## Organizing for change (OCP & DIP)

- **Open/Closed Principle.** Structure classes so that a new feature means **adding** a new class, not editing existing (tested, working) ones.
- **Dependency Inversion Principle.** Depend on **abstractions**, not concrete details. This decouples modules and — crucially — lets you swap in test doubles, so classes become isolable and testable.

## Takeaway

The exact same rule governs React components. A component that fetches data, transforms it, and renders it has three responsibilities. Push fetching/transforming into hooks or services and keep the component about **rendering**. Many small, focused units beat one omniscient one.
