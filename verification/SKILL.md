---
name: verification
description: Pre-completion verification gate. Use before claiming work is done, committing, or creating PRs. Prevents false completion claims.
disable-model-invocation: true
---

# Verification Before Completion

**NO COMPLETION CLAIMS WITHOUT FRESH VERIFICATION EVIDENCE.**

Adapted from [Superpowers](https://github.com/obra/superpowers) verification-before-completion and [Everything Claude Code](https://github.com/affaan-m/everything-claude-code) verification-loop.

## The Gate (run every time)

1. **BUILD**: Run project build command → must exit 0
2. **TYPECHECK**: `tsc --noEmit` / `mypy` / `cargo check` → 0 errors
3. **LINT**: Project linter → 0 errors (warnings OK if project allows)
4. **TEST**: Full test suite → all pass, check coverage
5. **SCAN**: `grep -rn "TODO\|FIXME\|HACK\|console\.log\|fmt\.Println\|print(" --include="*.go" --include="*.ts" --include="*.py" --include="*.rs" -- $(git diff --name-only HEAD)` → no debug artifacts in changed files
6. **DIFF**: `git diff --stat` → review every changed file for unintended changes

## Output Format

```
Verification Report
====================
Build:    [PASS/FAIL]
Types:    [PASS/FAIL] (X errors)
Lint:     [PASS/FAIL] (X warnings)
Tests:    [PASS/FAIL] (X/Y pass, Z% coverage)
Scan:     [PASS/FAIL] (X issues)
Diff:     [X files changed]

Overall:  [READY/NOT READY] for commit

Issues to fix:
1. ...
```

## Red Flags — STOP if you catch yourself:
- Saying "should work", "probably passes", "looks correct"
- Expressing satisfaction before running verification
- About to commit without running tests
- Trusting a sub-agent's "success" report without checking
- Using partial verification ("linter passed" ≠ "build passes")

**Evidence before claims. No exceptions.**
