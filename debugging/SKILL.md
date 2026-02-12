---
name: debugging
description: Systematic debugging process. Use when encountering bugs, test failures, or unexpected behavior — BEFORE attempting fixes.
---

# Systematic Debugging

**NO FIXES WITHOUT ROOT CAUSE INVESTIGATION FIRST.**

Adapted from [Superpowers](https://github.com/obra/superpowers) systematic-debugging.

## The Iron Law

If you haven't completed Phase 1, you cannot propose fixes. Guessing wastes time and creates new bugs.

## Phase 1: Investigate (MANDATORY)

1. **Read error messages completely** — stack traces, line numbers, error codes. Don't skip.
2. **Reproduce consistently** — write the exact steps. If you can't reproduce, you can't verify a fix.
3. **Isolate the scope** — binary search: which commit? which file? which function? which line?
4. **Form a hypothesis** — "I believe X causes Y because Z"

## Phase 2: Verify Hypothesis

- Add targeted logging/assertions to confirm your hypothesis
- If hypothesis is wrong, return to Phase 1. Don't guess again.

## Phase 3: Fix

- Fix the ROOT CAUSE, not the symptom
- Minimal change — don't refactor while debugging

## Phase 4: Verify Fix

- Reproduce original bug → confirm it's gone
- Run full test suite → no regressions
- Write a regression test if one doesn't exist

## Anti-Patterns Claude Does

| Bad | Good |
|-----|------|
| Change code and see if error goes away | Understand WHY it errors first |
| Fix the first thing that looks wrong | Confirm it's actually the cause |
| "Try this" without hypothesis | "I believe X because Y, testing with Z" |
| Multiple changes at once | One change, verify, then next |
| Skip regression test | Always add test for the bug |
