# JavaScript and TypeScript

## Structure

- Use one root `describe` for each file. Name it after the unit under test.
- Use nested `describe` blocks for each method or scenario.
- Use `it` or `test` as the repository does. If the repository has no convention, use `it`.

```ts
describe("Cart", () => {
  describe("total", () => {
    it("returns 0 for an empty cart", () => {
      const cart = new Cart(new PriceList());

      const total = cart.total();

      expect(total).toBe(0);
    });
  });
});
```

## Parameterized tests

Use `it.each` with a named case:

```ts
it.each([
  { name: "one item", items: ["a"], expected: 10 },
  { name: "two items", items: ["a", "b"], expected: 30 },
])("returns the sum for $name", ({ items, expected }) => {
  const cart = new Cart(priceList, items);

  const total = cart.total();

  expect(total).toBe(expected);
});
```

## Cleanup

Use `beforeEach`, `afterEach`, and `afterAll`.

## Fakes

- Clock: inject a clock, or use `vi.useFakeTimers()` or `jest.useFakeTimers()`.
- File system: `memfs`.

## Mutation tool

Stryker (`@stryker-mutator/core`). Use `--mutate` to limit the run to the changed files.

## Coverage tool

Vitest `--coverage` or Jest `--coverage`. Use c8 for other runners. Read the branch column of the report.
