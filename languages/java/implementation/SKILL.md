---
name: java-implementation
description: Java/Spring pitfalls — null handling, stream misuse, Spring DI mistakes. Load when writing or reviewing .java files.
---

# Java Implementation — What Claude Gets Wrong

## Null Handling
- **Use `Optional<T>` for return types that may be absent** — Claude often returns null instead
- Never pass `Optional` as a method parameter — it's for return types only
- `Objects.requireNonNull()` for fail-fast on constructor/method entry
- Prefer `Optional.map().orElse()` chains over `if (x != null)` nesting

## Stream API Mistakes
- **Don't reuse streams** — a stream can only be consumed once
- Prefer `stream().toList()` (Java 16+) over `stream().collect(Collectors.toList())`
- Side effects in `map()`/`filter()` are a bug — use `forEach()` or `peek()` (debug only)
- `flatMap` for nested collections, not nested `map` calls

## Spring Boot Pitfalls
- **`@Transactional` on private methods does nothing** — Spring proxies only intercept public methods
- `@Autowired` on fields is discouraged — use constructor injection
- `@Value` with missing properties throws at startup — always provide defaults or use `@ConfigurationProperties`
- `@RequestBody` without `@Valid` skips validation — Claude often forgets `@Valid`

## Common Bugs
- `==` on objects compares reference, not value — use `.equals()` (Claude knows this but still slips)
- Mutable collections from `List.of()` / `Map.of()` are actually immutable — `new ArrayList<>(List.of(...))` if mutation needed
- `String.format()` locale issues — use explicit `Locale` for number/date formatting
- Checked vs unchecked exceptions: wrap checked in `RuntimeException` at boundaries, don't propagate `throws` everywhere

## Build Verification
- `mvn compile` or `gradle build` → `mvn test` → `mvn checkstyle:check` or `./gradlew check`
- SpotBugs/PMD if configured in project
