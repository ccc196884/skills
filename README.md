# Skills

Portable AI agent skill pack. Clone → code → ship.

```bash
git clone https://github.com/ccc196884/skills.git .claude/skills
```

That's it. Your agent is now smarter.

## How it works

Each skill is loaded **on-demand** — only when relevant to what you're working on. No token bloat.

This follows [Anthropic's official best practices](https://code.claude.com/docs/en/best-practices):
> CLAUDE.md is loaded every session, so only include things that apply broadly. For domain knowledge or workflows that are only relevant sometimes, use **skills** instead. Claude loads them on demand without bloating every conversation.

## Skills

| Skill | Triggers when... | What it does |
|-------|-------------------|-------------|
| `go/` | Working with `.go` files | Go idioms, error handling, testing patterns |
| `typescript/` | Working with `.ts`/`.tsx` files | TS best practices, type safety, framework patterns |
| `python/` | Working with `.py` files | Pythonic patterns, typing, testing |
| `rust/` | Working with `.rs` files | Ownership, error handling, Cargo patterns |
| `testing/` | Writing or fixing tests | Test strategy, coverage, mocking guidelines |
| `pr-quality/` | Creating PRs | Pre-submit checklist, CI verification |
| `security/` | Security-sensitive code | Vulnerability patterns, input validation |
| `git-workflow/` | Git operations | Commit conventions, branch strategy |

## Philosophy

- **Curated, not collected** — Every skill is tested and proven useful
- **Minimal by default** — Each SKILL.md is concise; detailed refs in subdirectories
- **On-demand only** — Zero overhead when not needed
- **Portable** — Works with Claude Code, OpenClaw, or any agent supporting the [Agent Skills](https://agentskills.io) standard

## Contributing

PRs welcome. Each skill must:
1. Solve a real problem (not theoretical)
2. Be concise (if removing a line doesn't hurt, remove it)
3. Include a clear `description` in frontmatter

## License

MIT
