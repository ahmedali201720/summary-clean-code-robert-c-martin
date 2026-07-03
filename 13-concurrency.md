# Chapter 13 — Concurrency

> *Clean Code* by Robert C. Martin ("Uncle Bob"). Principles faithful to the original; examples in JS/TS/React.
> **Nav:** ← [12 Emergence](12-emergence.md) · [Index](00-index.md) · Next → [14 Successive Refinement](14-successive-refinement.md)

*Concurrency decouples what from when — and it is hard. Treat it with respect.*

---

## Why it's hard

Concurrency can improve throughput and structure, but it introduces a class of bugs that appear **rarely**, look like one-off glitches, and vanish the moment you attach a debugger. Several myths make it worse: "concurrency always improves performance" (not for small workloads), and "design doesn't change with concurrency" (it changes a lot).

## Defensive principles (mapped to JavaScript's async world)

- **Keep concurrency code separate.** Isolate the async/coordination logic from business logic so each can be understood and tested on its own. Concurrency is a single responsibility (SRP).
- **Limit access to shared data.** The fewer places touch shared mutable state, the fewer race conditions. Prefer copies and immutable data; give each task its own data where possible.
- **Keep critical sections small** and understand your primitives. In classic threads that's locks/atomics; in JS it's the single-threaded event loop, `Promise`s, and the message boundaries of Web/Worker threads.
- **Race conditions hide.** Don't wave off an intermittent failure as "a fluke" — it's usually a concurrency bug. Write tests that run the code many times, under load, on different configurations, to flush them out.

## The cleanest pattern: no shared mutable state

```ts
// smell: shared mutable state, interleaves across awaits
let total = 0;
async function add(id) {
  const n = await fetchAmount(id);
  total += n;             // read-modify-write races between tasks
}
await Promise.all(ids.map(add));
// total is unreliable

// clean: each task returns a value; combine at the end
const amounts = await Promise.all(ids.map(fetchAmount));
const total = amounts.reduce((a, b) => a + b, 0);
```

The same lesson applies to shared caches, module-level mutable variables, and unguarded writes to the same record from concurrent requests.

## Takeaway

The cleanest concurrent code has **no shared mutable state**. Let async tasks each compute and return a value, then combine results afterward, rather than reaching into shared variables mid-flight. When you must share, keep the guarded region tiny and test it under stress.
