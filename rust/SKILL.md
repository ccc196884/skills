---
name: rust
description: Rust development best practices and patterns. Loaded when working with .rs files.
---

# Rust

## Core Principles
- **Ownership is the language** — Think in terms of ownership, borrowing, lifetimes
- **Make illegal states unrepresentable** — Use the type system aggressively
- **Zero-cost abstractions** — Don't fear generics and traits

## Error Handling
- `Result<T, E>` for recoverable errors, `panic!` only for bugs
- Use `?` operator for propagation
- `thiserror` for library error types, `anyhow` for applications
- Implement `Display` and `Error` for custom error types

## Ownership & Borrowing
- Prefer borrowing (`&T`, `&mut T`) over ownership transfer
- Use `Clone` consciously — it's a code smell if overused
- `Cow<'_, str>` when you might or might not need to own
- Avoid `Rc`/`Arc` unless shared ownership is genuinely needed

## Patterns
- Builder pattern for complex constructors
- Newtype pattern for type safety (`struct UserId(u64)`)
- `impl From<T>` / `Into<T>` for conversions
- Iterator chains over manual loops
- `#[derive(...)]` — derive what you can

## Testing
- `#[cfg(test)] mod tests` in same file for unit tests
- `tests/` directory for integration tests
- `#[should_panic]` for expected failures
- Use `assert_eq!` with descriptive messages
- `proptest` or `quickcheck` for property-based testing

## Common Gotchas
- String types: `&str` for borrowing, `String` for owning
- `match` must be exhaustive — use `_` only when truly catch-all
- Async: `tokio` or `async-std`, not both
- Lifetimes: elision covers most cases; annotate only when compiler asks

## Build & Lint
- `cargo check` — fast type check
- `cargo clippy` — comprehensive linting
- `cargo test` — all tests
- `cargo fmt --check` — format check
- `cargo build --release` — optimized build
