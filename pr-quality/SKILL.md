---
name: pr-quality
description: Pre-PR quality gate. Invoke manually before creating any pull request.
disable-model-invocation: true
argument-hint: "[repo-path]"
---

# PR Quality Gate

**Do NOT create a PR until every step below passes.**

## Step 1: Discover CI checks
- Read `.github/workflows/` or equivalent CI config
- List every check CI runs (build, test, lint, format, typecheck)

## Step 2: Run every CI check locally
Execute in this order. Stop and fix on first failure:
1. Build: project-specific build command
2. Lint: project-specific linter
3. Format: project-specific formatter
4. Typecheck: if applicable
5. Test: full test suite

## Step 3: Verify no debug artifacts
```bash
grep -rn "TODO\|FIXME\|HACK\|XXX\|mock\|stub\|dummy\|console\.log\|fmt\.Println\|print(" \
  --include="*.go" --include="*.ts" --include="*.tsx" --include="*.py" --include="*.rs" \
  -- $(git diff --name-only HEAD)
```
If any hits in YOUR changed files: fix or justify each one.

## Step 4: PR description
- Title: clear, imperative mood
- Body: `Closes #XXXX`, what changed, why
- Screenshots/logs if behavior changed

## Step 5: Commit hygiene
- Sign-off (`-s`) if DCO required
- Rebase on upstream main, no merge commits
- Squash WIP commits
