---
name: typescript-implementation
description: TypeScript implementation pitfalls — type safety, any avoidance, React patterns. Load when writing new TS code or reviewing implementation (not test files).
---

# TypeScript Implementation — What Claude Gets Wrong

## Type Safety Mistakes
- **Never use `any`** — use `unknown` + type narrowing, or generic `<T>`
- **`as` casts are a code smell** — prefer discriminated unions or type guards
- **Avoid enums** — use `as const` objects or string union types (enums have runtime overhead and quirks)
- `satisfies` operator > type annotation when you want to check without widening

## Common Bugs Claude Introduces
- Using `||` for defaults when `??` is correct (`0` and `""` are falsy but valid)
- Forgetting `readonly` on arrays/objects that shouldn't be mutated
- Creating interfaces that should be `type` (unions, intersections, mapped types need `type`)
- Over-chaining `?.` — if 4+ levels deep, the data model needs fixing

## React Pitfalls (if applicable)
- Don't use `React.FC` — it's deprecated in community practice. Use plain function with typed props
- `children` type is `ReactNode`, not `JSX.Element` or `React.ReactElement`
- Hooks rules: no conditional `use*()` calls — Claude sometimes generates these
- Keys must be stable IDs, NEVER array index (unless static list)

## Build Verification
- `tsc --noEmit` → `eslint .` → `prettier --check .` → `npm test`
