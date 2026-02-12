---
name: git-workflow
description: Git workflow conventions for contributing to open source projects.
---

# Git Workflow

## Branch Naming
- `feat/{issue-number}-short-description` — new feature
- `fix/{issue-number}-short-description` — bug fix
- `docs/{description}` — documentation only
- `refactor/{description}` — code restructuring

## Commit Messages
- Format: `type: concise description`
- Types: `feat`, `fix`, `docs`, `test`, `refactor`, `chore`, `ci`
- Imperative mood: "add feature" not "added feature"
- Reference issues: `feat: add email validation (closes #123)`
- Keep first line under 72 characters

## Before Pushing
1. Rebase on upstream main: `git fetch upstream && git rebase upstream/main`
2. Resolve conflicts cleanly (don't merge, rebase)
3. Squash WIP commits into logical units
4. Verify all tests pass after rebase

## Pull Request Conventions
- One PR per issue/feature
- Fill in the PR template if one exists
- Link the issue: `Closes #XXXX`
- Keep PRs focused and reviewable (< 400 lines preferred)
- Respond to review comments promptly

## DCO Sign-Off
Some projects require Developer Certificate of Origin:
```bash
git commit -s -m "feat: add feature"
```
The `-s` flag adds `Signed-off-by: Name <email>` to the commit.

## Fork Workflow (Open Source)
1. Fork the repo
2. Clone your fork
3. Add upstream remote: `git remote add upstream <original-repo-url>`
4. Create feature branch from up-to-date main
5. Push to your fork, open PR against upstream
