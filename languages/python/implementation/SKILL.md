---
name: python-implementation
description: Python implementation pitfalls — type hints, mutable defaults, exception chaining. Load when writing new Python code or reviewing implementation (not test files).
---

# Python Implementation — What Claude Gets Wrong

## Type Hints (Claude frequently omits or misuses)
- **All function params and return types MUST be annotated** — no exceptions
- Use modern syntax: `str | None` not `Optional[str]`, `list[str]` not `List[str]` (3.10+)
- `TypedDict` for dict shapes, `dataclass` for data containers — Claude defaults to plain dicts too often
- `Protocol` for duck typing with type safety — Claude rarely suggests this

## Common Bugs Claude Introduces
- Mutable default arguments: `def f(items=[])` is a shared mutable — use `None` + `if items is None`
- Bare `except:` — always catch specific exceptions
- `is` vs `==`: use `is` only for `None`, `True`, `False` singletons
- String concatenation in loops — use `"".join()` or f-strings
- Forgetting `raise ... from err` — exception chains are lost without it

## Patterns Claude Should Prefer
- `pathlib.Path` over `os.path` — always
- `dataclasses` over manual `__init__` — unless attrs is already in use
- Context managers for any resource (files, connections, locks)

## Build Verification
- `ruff check .` → `ruff format --check .` → `mypy .` → `pytest -x`
