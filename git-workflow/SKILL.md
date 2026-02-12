---
name: git-workflow
description: Git workflow for open source contributions. Load when making commits or PRs to external repos.
---

# Git Workflow — OSS Contributions

## Fork Workflow
1. Fork → clone your fork → `git remote add upstream <original>`
2. Branch from up-to-date main: `git fetch upstream && git checkout -b feat/123-desc upstream/main`
3. Push to YOUR fork, PR against upstream

## Commit Messages
- Format: `type: concise imperative description`
- Types: `feat`, `fix`, `docs`, `test`, `refactor`, `chore`, `ci`
- Reference issues: `feat: add validation (closes #123)`
- First line < 72 chars

## Before Pushing
1. `git fetch upstream && git rebase upstream/main`
2. Resolve conflicts (rebase, don't merge)
3. Squash WIP commits into logical units
4. Run full test suite after rebase

## DCO Sign-Off
Many OSS projects require it:
```bash
git commit -s -m "feat: add feature"
```
Check CONTRIBUTING.md — if DCO is required and you forget `-s`, the CI will reject.
