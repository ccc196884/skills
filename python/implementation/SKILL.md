---
name: python-implementation
description: Python implementation best practices and patterns.
---

# Python Implementation

## Core Principles
- **Readability counts** — PEP 8 is the baseline
- **Explicit is better than implicit** — No magic
- **Type hints everywhere** — All function signatures annotated

## Type Hints
- All function params and return types annotated
- Use `str | None` (3.10+) over `Optional[str]`
- `list[str]` over `List[str]` (3.9+)
- `TypedDict` for dict shapes, `dataclass` for data containers
- `Protocol` for structural subtyping (duck typing with types)

## Error Handling
- Catch specific exceptions, never bare `except:`
- Custom exception classes inheriting from domain base
- Context managers (`with`) for resource management
- `raise ... from err` to preserve exception chains

## Patterns
- `dataclasses` or `attrs` over manual `__init__`
- `pathlib.Path` over `os.path`
- f-strings for formatting
- List/dict comprehensions when readable
- `enumerate()` over manual counter
- `collections.defaultdict`, `Counter` for common patterns

## Project Structure
- `pyproject.toml` for project config (PEP 621)
- `src/` layout for packages
- `__all__` in `__init__.py` for public API

## Build & Lint
- `ruff check .` — fast linting
- `ruff format .` — formatting
- `mypy .` — type checking
