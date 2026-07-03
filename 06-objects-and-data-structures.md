# Chapter 6 — Objects & Data Structures

> *Clean Code* by Robert C. Martin ("Uncle Bob"). Principles faithful to the original; examples in JS/TS/React.
> **Nav:** ← [05 Formatting](05-formatting.md) · [Index](00-index.md) · Next → [07 Error Handling](07-error-handling.md)

*Objects hide data behind behavior. Data structures expose data and have no behavior. Don't blur them.*

---

## Data abstraction

An object doesn't just expose its variables with getters/setters — that's not abstraction, it's a data structure wearing a disguise. A true object hides *how* it stores things and offers **behavior** instead. Expose the essence of the data, not its representation.

## The data/object anti-symmetry

This is the key insight:

- **Objects** expose behavior and hide data. → Easy to add new **types** without changing existing behavior; hard to add new **operations** (you must touch every class).
- **Data structures** expose data and have no behavior. → Easy to add new **operations** (write a new function); hard to add new **types** (you must touch every function).

They are opposites. Choose the one that matches how your code will grow. **Hybrids** — objects with public data *and* significant behavior — get the worst of both and should be avoided.

```ts
// smell: a hybrid — exposes internals AND adds logic
class Vehicle {
  fuelTankCapacity; fuelLevel;
  getPercentFuel() { return 100 * this.fuelLevel / this.fuelTankCapacity; }
}

// clean (object): hide the data, expose behavior
class Vehicle {
  #capacity; #level;
  percentFuelRemaining() { return 100 * this.#level / this.#capacity; }
}
```

For pure data — API payloads, DB rows, config — use plain objects or TypeScript `type`s as **DTOs** with no behavior. Don't bolt methods onto them.

```ts
type UserDTO = { id: string; email: string; createdAt: string };
```

## The Law of Demeter — "don't talk to strangers"

A method should only call methods on:

1. its own object,
2. objects passed in as parameters,
3. objects it creates,
4. its own direct fields.

Reaching through a chain — `a.getB().getC().doThing()`, a **train wreck** — couples you to the entire structure, so any change downstream breaks you.

```ts
// smell: train wreck
const dir = ctx.getOptions().getScratchDir().getAbsolutePath();

// clean: ask, don't traverse
const dir = ctx.scratchDirPath();  // ctx owns the knowledge of how to get it
```

## Takeaway

Decide, per module, whether you want an **object** (hide data, add behavior, easy to add types) or a **data structure / DTO** (expose data, no behavior, easy to add operations). Blurring the two is where tangled designs come from.
