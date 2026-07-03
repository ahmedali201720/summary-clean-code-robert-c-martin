# Chapter 2 — Meaningful Names

> *Clean Code* by Robert C. Martin ("Uncle Bob"). Principles faithful to the original; examples in JS/TS/React.
> **Nav:** ← [01 Clean Code](01-clean-code.md) · [Index](00-index.md) · Next → [03 Functions](03-functions.md)

*The name is the comment you can't get wrong. Spend your effort here.*

---

## Use intention-revealing names

A name should answer three questions: **why it exists**, **what it does**, and **how it's used**. If a name needs a comment to explain it, it isn't revealing intent.

```js
// smell: disinformation & noise
const d = 30;                    // what is d? what unit?
const list1 = users.filter(u => u.a);

function getThem(theList) {
  const list1 = [];
  for (const x of theList)
    if (x[0] === 4) list1.push(x);
  return list1;
}

// clean: intention-revealing
const elapsedTimeInDays = 30;
const activeUsers = users.filter(u => u.isActive);

const FLAGGED = 4;
function getFlaggedCells(board) {
  return board.filter(cell => cell.status === FLAGGED);
}
```

## The rules

- **Avoid disinformation.** Don't call it `accountList` unless it's actually a List. Avoid names that differ in tiny ways (`XYZControllerForHandlingOfStrings` vs `...StorageOfStrings`).
- **Make meaningful distinctions.** `a1, a2, a3` and noise words like `ProductInfo` / `ProductData` carry no information.
- **Use pronounceable names.** `genymdhms` → `generationTimestamp`. You have to talk about code with other humans.
- **Use searchable names.** A single letter is fine only as a local loop counter; anything you'll grep for needs a real name. Replace magic numbers with named constants.
- **Avoid encodings.** No Hungarian notation, no `m_` member prefixes, no `IShapeFactory` interface prefixes.
- **Avoid mental mapping.** Don't make the reader translate `r` into "the lowercased URL with host stripped."
- **Class names are nouns** (`Customer`, `WikiPage`, `Parser`). **Method names are verbs** (`deletePage`, `save`).
- **Don't be cute / don't pun.** `whack()` for "kill" is a private joke; using `add` for both concatenation and insertion is a pun. Say what you mean.
- **Pick one word per concept.** Don't mix `fetch`, `retrieve`, and `get` across the codebase for the same idea.
- **Use solution-domain names** (CS terms, pattern names) when readers are programmers, and **problem-domain names** when the concept is business logic.
- **Add meaningful context.** `state` alone is vague; `addrState` or an `Address` object makes it clear. But **don't add gratuitous context** — prefixing every class in a small app with `GSD` helps no one.

## In React

```tsx
// smell: vague props & handlers
function Card({ data, flag, cb }) {
  return <div onClick={cb}>{flag && <Badge/>}{data.n}</div>;
}

// clean: the prop names are the docs
function UserCard({ user, isVerified, onSelect }) {
  return (
    <div onClick={onSelect}>
      {isVerified && <VerifiedBadge/>}
      {user.name}
    </div>
  );
}
```

## Takeaway

Renaming is cheap and safe with modern tooling, so there's no excuse for a bad name to survive. Good names remove the *need* for comments — this is the highest-leverage cleanup you can do.
