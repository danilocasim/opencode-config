# Python Testing (pytest)

## Defaults

- Use `pytest`
- Prefer fixtures over setup/teardown
- Prefer `pytest.mark.parametrize` for case tables
- For async: `pytest-asyncio`

## Patterns

```python
import pytest

@pytest.mark.parametrize(
    "input,expected",
    [
        ("a", "A"),
        ("", ""),
    ],
)
def test_uppercase(input: str, expected: str) -> None:
    assert input.upper() == expected
```

## Error paths

```python
import pytest

def test_raises_on_invalid_input() -> None:
    with pytest.raises(ValueError, match="invalid"):
        parse_date("nope")
```

## Isolation

- Use `monkeypatch` for environment and globals
- Use `freezegun` or controlled clocks if needed
