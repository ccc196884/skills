---
name: go-implementation
description: Go-specific pitfalls and patterns Claude often gets wrong. Load when writing or reviewing .go files.
---

# Go Implementation — What Claude Gets Wrong

## Error Handling (common mistakes)
- Always wrap with context: `fmt.Errorf("doing X: %w", err)` — not bare `return err`
- Use `%w` (wrappable) vs `%v` (opaque) consciously — default to `%w`
- Never `_ = someFunc()` to silence errors in production code

## Gotchas Claude Frequently Hits
- **nil interface trap**: `var err *MyError = nil; var i error = err; i != nil` is TRUE
- **Slice append**: `append` may return a new backing array — always reassign: `s = append(s, v)`
- **defer args**: `defer fmt.Println(x)` captures `x` NOW, not at defer time
- **Loop var in goroutines**: Pre-Go 1.22, loop vars are shared — capture locally or use Go 1.22+
- **init() ordering**: Avoid `init()` when possible; it makes testing and reasoning harder

## Patterns Claude Should Prefer
- Functional options over config structs for public APIs with optional params
- `Accept interfaces, return structs` — but don't create interfaces preemptively
- Table-driven validation over deeply nested if/else

## Build Verification
- `go vet ./...` then `golangci-lint run` then `go test -race ./...`
- Check for `//nolint` directives — each must have a justification comment
