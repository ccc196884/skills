---
name: rust-testing
description: Rust testing patterns and conventions.
---

# Rust Testing

## Philosophy
- Unit tests live in the same file: `#[cfg(test)] mod tests`
- Integration tests in `tests/` directory
- Compile-time guarantees reduce need for runtime tests — focus on logic

## Unit Tests
```rust
#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn parse_valid_input() {
        let result = parse("hello").unwrap();
        assert_eq!(result, Expected::Hello);
    }

    #[test]
    #[should_panic(expected = "empty input")]
    fn parse_empty_panics() {
        parse("");
    }
}
```

## Conventions
- `#[test]` for each test function
- `assert_eq!(got, want)` with descriptive variable names
- `#[should_panic]` for expected panics
- Use `Result<(), E>` return type for tests that use `?`
- `#[ignore]` for slow tests, run with `cargo test -- --ignored`

## Integration Tests
- `tests/` directory, each file is a separate crate
- Can only test public API
- Shared helpers in `tests/common/mod.rs`

## Property-Based Testing
- `proptest` or `quickcheck` for generative testing
- Useful for parsers, serializers, mathematical properties

## Benchmarks
- `criterion` crate for benchmarks
- `cargo bench` to run
- Compare with statistical analysis

## Commands
- `cargo test` — all unit + integration tests
- `cargo test -- --test-threads=1` — serial execution
- `cargo test {name}` — filter by test name
