# Chapter 9 — Unit Tests

> *Clean Code* by Robert C. Martin ("Uncle Bob"). Principles faithful to the original; examples in JS/TS/React.
> **Nav:** ← [08 Boundaries](08-boundaries.md) · [Index](00-index.md) · Next → [10 Classes](10-classes.md)

*Test code is not second-class. Dirty tests are worse than no tests — they rot and get abandoned.*

---

## The Three Laws of TDD

1. Write **no production code** until you have a failing test that requires it.
2. Write **no more of a test** than is sufficient to fail (not compiling counts as failing).
3. Write **no more production code** than is sufficient to pass the current failing test.

Followed strictly, this cycle produces dozens of tests a day covering essentially all your code.

## Keeping tests clean

Tests must change as production code changes. If they're unreadable and brittle, maintaining them becomes a burden, so they get neglected, then deleted — and now production code has no safety net and starts to rot too.

> Test code is just as important as production code. It requires thought, design, and care.

The single most important quality of a test is **readability** — even more than in production code.

## F.I.R.S.T

- **Fast** — so you run them constantly.
- **Independent** — no test depends on another's state or ordering.
- **Repeatable** — same result on any machine, no reliance on network/clock/environment.
- **Self-validating** — a boolean pass/fail; no reading logs by hand.
- **Timely** — written just before the production code they cover.

## One concept per test

Prefer a single logical assertion, and don't test several unrelated concepts in one test. Use **test-data builders** to keep setup readable.

```js
// smell: many concepts, opaque
test('user', () => {
  const u = new User('a@b.co');
  expect(u.email).toBe('a@b.co');
  u.deactivate();
  expect(u.active).toBe(false);
  u.activate();
  expect(u.active).toBe(true);
});

// clean: one concept each, names describe behavior
const aUser = () => new User('a@b.co');

test('new user is active', () => {
  expect(aUser().active).toBe(true);
});

test('deactivate turns the user off', () => {
  const u = aUser();
  u.deactivate();
  expect(u.active).toBe(false);
});
```

## In React

This is **Testing Library**'s whole philosophy: test what the *user* experiences, not implementation details.

```tsx
test('shows an error when email is empty', async () => {
  render(<SignupForm />);
  await userEvent.click(screen.getByRole('button', { name: /sign up/i }));
  expect(screen.getByText(/email is required/i)).toBeInTheDocument();
});
```

Query by role/label/text, drive with `userEvent`, assert on visible output — one behavior per test.

## Takeaway

Clean tests give you the freedom to refactor fearlessly. That freedom is the whole point (see Ch. 12): tests are what let good design *emerge* without fear of breaking things.
