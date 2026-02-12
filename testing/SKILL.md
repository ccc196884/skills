---
name: testing
description: Test writing best practices. Loaded when writing, fixing, or reviewing tests.
---

# Testing

## Core Principles
- **Test behavior, not implementation** — Tests should survive refactoring
- **One assertion per concept** — Each test verifies one thing
- **Tests are documentation** — Name them so a stranger understands the intent

## Test Naming
- Pattern: `Test_{Function}_{Scenario}_{ExpectedResult}`
- Examples:
  - `Test_ValidateEmail_EmptyString_ReturnsError`
  - `test_parse_config_missing_file_raises_file_not_found`
  - `it("returns 404 when user does not exist")`

## Structure: Arrange-Act-Assert
```
// Arrange: set up test data and dependencies
// Act: call the function under test
// Assert: verify the result
```

## What to Test
- Happy path (expected inputs → expected outputs)
- Edge cases (empty, nil/null, boundary values, max length)
- Error cases (invalid input, network failures, permission denied)
- Concurrency (if applicable — race conditions, deadlocks)

## What NOT to Test
- Private/internal methods directly (test through public API)
- Third-party library internals
- Trivial getters/setters
- Implementation details that may change

## Mocking Guidelines
- Mock at **boundaries** (HTTP clients, databases, file system)
- Prefer real implementations when feasible (in-memory DB, test server)
- Never mock the thing you're testing
- If you need more than 3 mocks, the design may need refactoring

## Test Data
- Use factory functions or builders for test objects
- Keep test data close to the test
- Use `testdata/` or `fixtures/` directories for file-based test data
- Never share mutable state between tests

## Coverage
- Aim for meaningful coverage, not 100%
- Uncovered code = untested behavior (review if intentional)
- Branch coverage matters more than line coverage
