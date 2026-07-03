# Chapter 8 — Boundaries

> *Clean Code* by Robert C. Martin ("Uncle Bob"). Principles faithful to the original; examples in JS/TS/React.
> **Nav:** ← [07 Error Handling](07-error-handling.md) · [Index](00-index.md) · Next → [09 Unit Tests](09-unit-tests.md)

*Keep third-party code at arm's length. Own the seam between their world and yours.*

---

## The core idea

Third-party APIs are broad, general, and can change out from under you. Your application needs only a narrow, stable slice of them. If a library's types and calls spread through your whole codebase, then a breaking upgrade — or a decision to switch vendors — becomes a hundred-file edit.

**Wrap** external code behind an interface *you* control. Then the vendor lives in one file, and change is contained there.

```ts
// smell: the vendor bleeds through the app
// axios calls scattered across the codebase
const res = await axios.get(`https://api.x.com/u/${id}`, {
  headers: { Authorization: token },
});
const user = res.data;
// change the HTTP library ⇒ change 200 files

// clean: one seam you control
// http-client.ts — the ONLY file that knows about axios
export const api = {
  getUser: (id: string) => http(`/u/${id}`).then(r => r.data),
};
// app code calls api.getUser(id) — vendor-agnostic
```

## Learning tests

When adopting a new library, don't read the docs and hope. Write small **learning tests** that call the library and assert how it behaves. Benefits:

- You learn the API faster by experimenting against real assertions.
- The tests become an **early-warning system**: when you upgrade the library and its behavior changes, your learning tests fail *before* production does.

## Boundaries for code that doesn't exist yet

When you depend on an API another team hasn't built, define the **interface you wish you had**, code against it, and back it with a fake for now. When the real thing lands, you write one adapter — the rest of your code never knew the difference.

## Takeaway

Your code should depend on *your* abstraction, not on Stripe / Axios / Prisma directly. The wrapper is cheap insurance against a dependency you don't control.
