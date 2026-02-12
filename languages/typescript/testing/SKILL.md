---
name: typescript-testing
description: TypeScript/JavaScript testing mistakes Claude makes. Load when writing or reviewing test files (*.test.ts, *.spec.ts).
---

# TypeScript Testing — What Claude Gets Wrong

## Critical Mistakes
- **Test behavior, not implementation** — don't assert on internal state or mock internals
- **Don't over-mock** — if you need 5+ mocks, the code needs refactoring, not more mocks
- **Always restore mocks** — `afterEach(() => vi.restoreAllMocks())` or Jest equivalent
- **Snapshot tests are a trap** — use sparingly; they pass silently when updated without review

## Framework Choice
- Check `package.json` first — use whatever the project already uses (Vitest, Jest, Mocha)
- Don't introduce a new test framework without checking existing setup

## Component Testing (React/Vue)
- Use Testing Library — query by role/label, NOT by CSS class or test-id
- `screen.getByRole("button", { name: "Submit" })` > `screen.getByTestId("submit-btn")`
- Test user interactions: click, type, submit — not component internals
- `waitFor` for async updates, not arbitrary `setTimeout`

## Async Testing
- Always `await` async assertions: `await expect(fn()).rejects.toThrow()`
- Missing `await` = test passes without actually running the assertion
