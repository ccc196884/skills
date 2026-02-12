---
name: python-testing
description: Python testing mistakes Claude makes. Load when writing or reviewing test files (test_*.py, *_test.py).
---

# Python Testing — What Claude Gets Wrong

## Critical Mistakes
- **Use pytest, not unittest** — unless the project already uses unittest
- **Don't create unnecessary conftest.py** — keep fixtures close to tests, not in a global conftest
- **Never use `mock.patch` on the thing you're testing** — mock dependencies, not the subject

## pytest Patterns
- `@pytest.mark.parametrize` for table-driven tests — Claude sometimes writes separate test functions instead
- Use `pytest.raises(ExactException, match="pattern")` — not bare `pytest.raises(Exception)`
- `tmp_path` fixture for temp files — don't create manual temp dirs
- `monkeypatch` for env vars — not `os.environ` manipulation

## Mocking
- Patch where the thing is USED, not where it's DEFINED: `mock.patch("mymodule.requests.get")` not `mock.patch("requests.get")`
- Prefer dependency injection over patching — if you can refactor to inject, do it
- `responses` or `httpx_mock` for HTTP — don't hand-roll request mocks

## Async Testing
- Use `pytest-asyncio` with `@pytest.mark.asyncio`
- `async def test_*` — Claude sometimes forgets the async marker
