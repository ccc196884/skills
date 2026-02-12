---
name: typescript-testing
description: TypeScript/JavaScript testing patterns and conventions.
---

# TypeScript Testing

## Philosophy
- **Test behavior, not implementation** — Tests survive refactoring
- Component tests: test what the user sees, not internal state
- Mock at module boundaries (HTTP, DB), not internals

## Frameworks
- **Vitest** (preferred) or **Jest** for unit/integration
- **Testing Library** for component tests
- **Playwright** or **Cypress** for E2E

## Patterns
```typescript
describe("UserService", () => {
  it("returns user by ID", async () => {
    const user = await service.findById("123");
    expect(user.name).toBe("Alice");
  });

  it("throws NotFoundError for unknown ID", async () => {
    await expect(service.findById("unknown"))
      .rejects.toThrow(NotFoundError);
  });
});
```

## Conventions
- `describe/it` blocks with clear human-readable descriptions
- One concept per `it` block
- Use `beforeEach` for shared setup, not shared mutable state
- Prefer `toEqual` for objects, `toBe` for primitives
- Snapshot tests: use sparingly, update intentionally

## Mocking
- `vi.mock()` / `jest.mock()` for module-level mocking
- `vi.spyOn()` to observe without replacing
- Always restore mocks: `afterEach(() => vi.restoreAllMocks())`
- Prefer dependency injection over module mocking when possible

## Coverage
- `vitest run --coverage` / `jest --coverage`
- Focus on branch coverage over line coverage
- Untested branches = untested behavior
