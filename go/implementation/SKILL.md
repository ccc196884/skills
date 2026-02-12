---
name: go-implementation
description: Go implementation best practices, idioms, and patterns.
---

# Go Implementation

## Core Principles
- **Simplicity over cleverness** — Go rewards boring, readable code
- **Errors are values** — Handle them explicitly, never ignore
- **Composition over inheritance** — Use interfaces and embedding

## Error Handling
- Always check errors: `if err != nil { return fmt.Errorf("context: %w", err) }`
- Wrap errors with `%w` for unwrapping, `%v` when wrapping is not needed
- Use `errors.Is()` / `errors.As()` for checking, not string comparison
- Define sentinel errors as package-level `var ErrNotFound = errors.New("not found")`

## Naming
- Short, lowercase package names (`http`, `os`, not `httpUtils`)
- Exported: `PascalCase`. Unexported: `camelCase`
- Interfaces: single-method → `-er` suffix (`Reader`, `Writer`)
- Avoid stuttering: `http.Client` not `http.HTTPClient`
- Acronyms all caps: `ID`, `URL`, `HTTP`

## Patterns
- Accept interfaces, return structs
- Use `context.Context` as first param for cancellation/timeouts
- `defer` for cleanup (files, locks, connections)
- Channel direction in function signatures: `func consume(ch <-chan int)`
- Functional options for configurable constructors

## Common Gotchas
- Loop variable capture in goroutines (use local copy or Go 1.22+ loop semantics)
- `nil` interface vs `nil` concrete type are not equal
- Slice append may or may not allocate — don't assume capacity
- `defer` evaluates args immediately, executes later

## Build & Lint
- `go vet ./...` — catch common mistakes
- `golangci-lint run` — comprehensive linting
- `go build ./...` — verify compilation
