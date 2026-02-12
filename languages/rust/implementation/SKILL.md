---
name: rust-implementation
description: Rust implementation pitfalls — ownership, clone abuse, error type choice. Load when writing new Rust code or reviewing implementation (not test code).
---

# Rust Implementation — What Claude Gets Wrong

## Ownership Mistakes
- **Don't `.clone()` to satisfy the borrow checker** — fix the ownership model first. Clone is a last resort.
- **Don't use `Rc`/`Arc` by default** — only when shared ownership is genuinely required
- `Cow<'_, str>` when you might or might not need to own — Claude rarely suggests this
- Prefer `&str` in function params, `String` in struct fields

## Error Handling
- `thiserror` for libraries (typed errors), `anyhow` for applications (ergonomic errors) — don't mix them up
- Always `?` over `unwrap()` in non-test code — Claude sometimes uses `unwrap` for convenience
- `unwrap()` is acceptable in tests and examples only
- Use `#[error("context: {source}")]` with `thiserror` — not bare error messages

## Common Bugs
- `match` exhaustiveness: don't use `_ =>` catch-all unless truly generic — enumerate variants explicitly
- Forgetting `Send + Sync` bounds on async code — surfaces as confusing compile errors
- Using `String` where `&str` suffices — unnecessary allocation
- `Vec::new()` + push loop when `collect()` from iterator is cleaner

## Build Verification
- `cargo check` → `cargo clippy -- -D warnings` → `cargo test` → `cargo fmt --check`
- Treat clippy warnings as errors (`-D warnings`)
