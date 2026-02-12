---
name: typescript
description: TypeScript development best practices and patterns. Loaded when working with .ts/.tsx files.
---

# TypeScript

## Core Principles
- **Type safety first** — Avoid `any`; use `unknown` when type is truly unknown
- **Strict mode always** — `"strict": true` in tsconfig.json
- **Infer when obvious, annotate when not** — Let TS do its job

## Types
- Prefer `interface` for object shapes (extendable), `type` for unions/intersections
- Use discriminated unions over type assertions
- `readonly` for immutable properties
- Use `as const` for literal types
- Avoid enums — prefer `const` objects or union types

## Error Handling
- Use typed errors or Result types over throwing
- If throwing, throw `Error` subclasses, never strings
- `try/catch` at boundaries, not everywhere

## Patterns
- Use `satisfies` operator for type checking without widening
- Prefer `Map`/`Set` over plain objects for dynamic keys
- Use `Partial<T>`, `Pick<T>`, `Omit<T>` utility types
- Nullish coalescing `??` over logical OR `||` for defaults
- Optional chaining `?.` — but don't chain more than 3 levels

## React (if applicable)
- Functional components only
- Props interface named `{ComponentName}Props`
- Use `ReactNode` for children type, not `JSX.Element`
- Custom hooks: prefix with `use`, return tuple or object
- Avoid prop drilling — use context or composition

## Testing
- Jest or Vitest for unit tests
- Testing Library for component tests — test behavior, not implementation
- `describe/it` blocks with clear descriptions
- Mock at module boundaries, not internals

## Build & Lint
- `tsc --noEmit` — type check without build
- `eslint .` — lint
- `prettier --check .` — format check
- `npm test` / `npx vitest run` — tests
