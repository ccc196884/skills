---
name: tdd
description: Test-driven development workflow. Use when writing new features or fixing bugs — write tests FIRST, then implement.
---

# Test-Driven Development

**Tests BEFORE code. Red → Green → Refactor.**

Adapted from [Everything Claude Code](https://github.com/affaan-m/everything-claude-code) tdd-workflow and [Superpowers](https://github.com/obra/superpowers) test-driven-development.

## The Cycle

### 1. RED — Write a failing test
- Write ONE test that describes the desired behavior
- Run it → it MUST fail (if it passes, the test is wrong or the feature already exists)
- The test name describes the behavior: `test_empty_input_returns_error`

### 2. GREEN — Write minimal code to pass
- Write the MINIMUM code to make the test pass
- No premature optimization, no extra features
- Run the test → it must pass

### 3. REFACTOR — Clean up
- Improve code quality without changing behavior
- Run tests → still green
- Commit

## When Claude Skips TDD (don't)

| Excuse | Reality |
|--------|---------|
| "I'll write tests after" | You won't, or they'll be shallow |
| "This is too simple for tests" | Simple code has edge cases too |
| "Tests slow me down" | Debugging without tests slows you more |
| "I'll just manually test" | Manual testing doesn't persist |

## What to Test

- **Happy path**: expected input → expected output
- **Edge cases**: empty, nil/null, zero, max, boundary
- **Error cases**: invalid input, missing data, network failure
- **Regression**: any bug you fix gets a test

## Red-Green Verification

When claiming a regression test works:
```
1. Write test → Run → MUST FAIL (proves test catches the bug)
2. Apply fix → Run → MUST PASS (proves fix works)
3. Revert fix → Run → MUST FAIL AGAIN (proves test is real)
4. Restore fix → Run → PASS → Commit
```

Skipping the revert step = the test might be meaningless.
