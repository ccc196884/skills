---
name: pr-quality
description: Pre-PR quality checklist. Use before creating any pull request to ensure CI passes and code is production-ready.
disable-model-invocation: true
---

# PR Quality Gate

**Run this checklist before creating ANY pull request. Do not skip steps.**

## Step 1: Read the CI Configuration
- Read `.github/workflows/` (or `.gitlab-ci.yml`, `Makefile`, etc.)
- Identify ALL checks that CI runs (build, test, lint, format, typecheck)
- Run each check locally in the same order

## Step 2: Build Verification
- [ ] Project builds without errors
- [ ] No compiler warnings (treat warnings as errors)

## Step 3: Test Verification
- [ ] ALL existing tests pass
- [ ] New code has tests (unit + integration where appropriate)
- [ ] `grep -rn "TODO\|FIXME\|HACK\|XXX" --include="*.go" --include="*.ts" --include="*.py" --include="*.rs"` — no unresolved items in your changes

## Step 4: Code Cleanliness
- [ ] No mock/stub/dummy data in production code
- [ ] No hardcoded test values in production code
- [ ] No commented-out code blocks
- [ ] No debug print statements (`fmt.Println`, `console.log`, `print()`)
- [ ] No placeholder implementations (`// TODO: implement`)

## Step 5: Lint & Format
- [ ] Linter passes with zero warnings
- [ ] Code is formatted per project conventions
- [ ] Import ordering follows project conventions

## Step 6: PR Description
- [ ] Clear title describing the change
- [ ] References the issue: `Closes #XXXX` or `Fixes #XXXX`
- [ ] Describes what changed and why
- [ ] Screenshots/logs for UI or behavior changes
- [ ] Breaking changes noted (if any)

## Step 7: Commit Hygiene
- [ ] Commits are signed off (`-s` flag) if DCO required
- [ ] Commit messages are descriptive
- [ ] No merge commits (rebase if needed)

## If ANY check fails: FIX IT before creating the PR. Never submit a PR that you know will fail CI.
