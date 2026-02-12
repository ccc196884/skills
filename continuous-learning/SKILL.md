---
name: continuous-learning
description: Learn from mistakes and evolve skills over time. Use after a PR is rejected, a bug is found in shipped code, or a bounty is lost.
---

# Continuous Learning

**Every mistake is a skill improvement opportunity.**

Adapted from [Compound Engineering Plugin](https://github.com/EveryInc/compound-engineering-plugin) and [Everything Claude Code](https://github.com/affaan-m/everything-claude-code) continuous-learning-v2.

## When to Trigger

- PR rejected or CI failed
- Bug found in code you wrote
- Bounty lost to a competitor
- Review feedback received
- Pattern of repeated mistakes noticed

## The Learning Loop

### 1. Capture (immediately after failure)
- What went wrong? (specific, not vague)
- What was the root cause?
- What should have been done differently?

### 2. Record
Add to the relevant skill file or create a new entry:
```markdown
## Lessons Learned
- YYYY-MM-DD: [specific mistake] → [what to do instead]
```

Or for project-specific lessons, add to `memory/` files.

### 3. Improve
- If a mistake pattern appears 2+ times → update the relevant SKILL.md
- If a new category of mistake → consider creating a new skill
- If a tool/process could have caught it → add to verification checklist

## What to Track

| Category | Example | Where to Record |
|----------|---------|-----------------|
| Language pitfall | Used `==` instead of `.equals()` in Java | `languages/java/implementation/SKILL.md` |
| Process failure | Submitted PR without running CI locally | `pr-quality/SKILL.md` |
| Architecture mistake | Didn't check existing patterns before coding | `debugging/SKILL.md` |
| Bounty-specific | Missed /attempt comments on Algora | `memory/bounty-strategy.md` |

## Anti-Pattern: Blame Without Learning

❌ "That was a stupid mistake"
✅ "That mistake reveals a gap in my checklist — adding it now"

The goal is not to feel bad. The goal is to never make the same mistake twice.
