---
name: go-testing
description: Go testing mistakes Claude makes. Load when writing or reviewing Go test files (*_test.go).
---

# Go Testing — What Claude Gets Wrong

## Critical Mistakes to Avoid
- **Never skip `t.Helper()`** in test helpers — stack traces become useless without it
- **Never use `assert` libraries by default** — use standard `t.Errorf`/`t.Fatalf` unless the project already uses one
- **Don't mock everything** — Go idiom is real implementations with interfaces only at boundaries (DB, HTTP, filesystem)
- **Don't forget `t.Parallel()`** where safe — but never with shared mutable state

## Table-Driven Test Template
Use this structure. Don't deviate:
```go
for _, tt := range tests {
    t.Run(tt.name, func(t *testing.T) {
        // arrange → act → assert
    })
}
```
- Each test case MUST have a `name` field
- Use `wantErr bool` pattern for error cases
- `got`/`want` naming for actual/expected

## Gotchas
- `testdata/` is magic — `go build` ignores it, use for fixtures
- `//go:build integration` tag for slow tests — don't mix with unit tests
- `TestMain` runs ONCE per package, not per test — use for expensive shared setup only
- `-count=1` disables test caching — use in CI

## Race Detection
- `go test -race ./...` is NON-NEGOTIABLE in CI
- If a test can't run with `-race`, the code has a bug, not the test
