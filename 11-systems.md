# Chapter 11 — Systems

> *Clean Code* by Robert C. Martin ("Uncle Bob"). Principles faithful to the original; examples in JS/TS/React.
> **Nav:** ← [10 Classes](10-classes.md) · [Index](00-index.md) · Next → [12 Emergence](12-emergence.md)

*Separate constructing a system from using it. Wiring is a concern of its own.*

---

## Separate construction from use

Startup — deciding which concrete objects to build and how to connect them — is a **different responsibility** from the runtime logic that uses those objects. When an object constructs its own dependencies on demand (`new PostgresClient(...)` inside a service), it hard-wires that choice and blocks testing.

Move construction to a dedicated place: a **`main` / composition root**, a factory, or a **dependency-injection** setup. The rest of the app then *receives* its dependencies and never reaches out for them.

```ts
// smell: the object wires its own dependencies
class OrderService {
  constructor() {
    this.db = new PostgresClient(env.URL);
    this.mail = new SendgridMailer(env.KEY);
  }
}
// can't test without a real DB and a real Sendgrid account

// clean: dependencies injected at the edge
class OrderService {
  constructor(private db: Db, private mailer: Mailer) {}
}

// composition root (main.ts)
const svc = new OrderService(realDb, realMailer);
// tests pass fakes — no network needed
```

## Scaling up

You can't design a whole system correctly up front, any more than a city is designed down to the last outlet. Systems should be able to **grow incrementally**, provided we keep concerns properly separated. Clean architecture lets you defer decisions and add capability without rewrites.

## Defer decisions to the last responsible moment

Don't commit early to a database, a framework detail, or a concrete implementation you don't yet need. Keep those decisions behind abstractions so you can decide when you have the most information — and change your mind cheaply.

## Takeaway

In React, this same idea shows up as **Context / provider composition** and passing clients in as props or through providers, rather than importing singletons deep in the component tree. Keep the "how it's built and wired" layer thin, explicit, and separate from the "what it does" layer.
