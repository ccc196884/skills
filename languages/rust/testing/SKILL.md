---
name: rust-testing
description: Rust test pitfalls — cfg(test) placement, integration vs unit, should_panic. Load only when writing or reviewing #[test] or tests/ directory code.
---

# Rust Testing — What Claude Gets Wrong

## Critical Mistakes
- **Tests go in `#[cfg(test)] mod tests` in the SAME file** — don't create separate test files for unit tests
- **`tests/` directory is for integration tests ONLY** — tests public API from outside the crate
- **`unwrap()` is fine in tests** — but `expect("reason")` is better for debugging failures
- Don't import `use super::*` if you can import specific items

## Patterns
```rust
#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn valid_input_returns_ok() {
        let result = parse("valid").expect("should parse");
        assert_eq!(result.value, 42);
    }

    #[test]
    fn empty_input_returns_error() {
        assert!(parse("").is_err());
    }
}
```

## Gotchas
- `#[should_panic(expected = "substring")]` — the `expected` is a substring match, not exact
- `#[ignore]` for slow tests — run with `cargo test -- --ignored`
- `cargo test` runs BOTH unit and integration tests — use `--lib` for unit only
- Test binary names can conflict — each `tests/*.rs` file is a separate binary

## Async Tests
- Use `#[tokio::test]` for async tests — Claude sometimes forgets the macro
- `tokio::test` creates a runtime per test — don't create your own
