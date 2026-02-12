---
name: python-testing
description: Python testing patterns and conventions.
---

# Python Testing

## Philosophy
- **pytest over unittest** — Less boilerplate, better assertions
- Test through public API, not private methods
- Fast tests run first, slow tests tagged separately

## pytest Conventions
```python
def test_validate_email_valid_input():
    assert validate_email("user@example.com") is True

def test_validate_email_empty_string_raises():
    with pytest.raises(ValueError, match="empty"):
        validate_email("")

@pytest.mark.parametrize("input,expected", [
    ("hello", "HELLO"),
    ("", ""),
    ("123", "123"),
])
def test_transform(input, expected):
    assert transform(input) == expected
```

## Fixtures
- Use `@pytest.fixture` for setup/teardown
- `tmp_path` for temp files, `monkeypatch` for env vars
- Scope fixtures appropriately: `function` (default), `module`, `session`
- Avoid `conftest.py` bloat — keep fixtures close to tests

## Mocking
- `unittest.mock.patch` at module boundaries
- `MagicMock` / `AsyncMock` for complex interfaces
- Prefer dependency injection over patching internals
- `responses` or `httpx_mock` for HTTP mocking

## Coverage
- `pytest --cov=src --cov-report=term-missing`
- Focus on meaningful paths, not 100%
- Use `# pragma: no cover` sparingly and with justification
