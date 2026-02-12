---
name: go-testing
description: Go testing patterns and conventions.
---

# Go Testing

## Philosophy
- Go tests live next to the code (`foo_test.go` beside `foo.go`)
- Prefer real implementations over mocks — use interfaces at boundaries only
- Tests should be fast, independent, and deterministic

## Table-Driven Tests
```go
tests := []struct {
    name    string
    input   string
    want    string
    wantErr bool
}{
    {"valid input", "hello", "HELLO", false},
    {"empty input", "", "", true},
}
for _, tt := range tests {
    t.Run(tt.name, func(t *testing.T) {
        got, err := Transform(tt.input)
        if (err != nil) != tt.wantErr {
            t.Errorf("error = %v, wantErr %v", err, tt.wantErr)
            return
        }
        if got != tt.want {
            t.Errorf("got %q, want %q", got, tt.want)
        }
    })
}
```

## Conventions
- Use `t.Run()` for subtests — enables selective test execution
- Use `t.Helper()` in test helper functions
- `testdata/` directory for fixtures (ignored by `go build`)
- `t.Parallel()` for tests that can run concurrently
- `t.Cleanup()` for teardown

## Race Detection
- Always run `go test -race ./...` in CI
- Design for concurrency safety from the start

## Integration Tests
- Use build tags: `//go:build integration`
- Separate from unit tests: `go test -tags=integration ./...`
- Use `TestMain(m *testing.M)` for shared setup/teardown

## Benchmarks
- `func Benchmark_{Name}(b *testing.B)` with `b.N` loop
- `go test -bench=. -benchmem` for memory allocation stats
- Compare with `benchstat`
