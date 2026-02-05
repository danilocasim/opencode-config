---
name: python
description: Python 3.12+ conventions with strict typing (2024-2026)
---

# Python Conventions (Python 3.12+)

## Type Hints (Required)
```python
def greet(name: str, times: int = 1) -> str:
    return f"Hello, {name}!" * times
```

- **Type hints everywhere** - parameters, returns, class attributes
- **Use `mypy --strict`** or `pyright` for type checking
- **No `Any`** unless truly necessary

## Modern Syntax (3.10+)
- **Match statements**: `match value: case pattern:` (3.10+)
- **Union syntax**: `str | None` over `Optional[str]` (3.10+)
- **Type parameter syntax**: `def func[T](x: T) -> T:` (3.12+)
- **F-strings**: Always, including `f"{value=}"` for debugging

## Data Structures
- **dataclasses**: For mutable data containers
- **frozen dataclasses**: `@dataclass(frozen=True)` for immutable
- **NamedTuple**: For lightweight immutable records
- **TypedDict**: For typed dictionaries
- **Pydantic**: For validation and serialization

```python
from dataclasses import dataclass

@dataclass(frozen=True, slots=True)
class User:
    id: int
    name: str
    email: str | None = None
```

## Functions
- **Keyword-only args**: `def f(*, name: str)` for clarity
- **Positional-only args**: `def f(x, /, y)` for flexibility (3.8+)
- **Default to immutable defaults**: Never `def f(items=[]):`
- **Single responsibility** - functions do one thing

## Error Handling
- **Specific exceptions** over bare `except:`
- **Custom exceptions** for domain errors
- **Context managers** for resource cleanup
- **Exception groups** for concurrent errors (3.11+)

```python
class UserNotFoundError(Exception):
    def __init__(self, user_id: int) -> None:
        self.user_id = user_id
        super().__init__(f"User {user_id} not found")
```

## Async
- **`async`/`await`** for I/O-bound operations
- **`asyncio.TaskGroup`** for concurrent tasks (3.11+)
- **Never block the event loop**

## Project Structure
```
src/
  mypackage/
    __init__.py
    module.py
tests/
  test_module.py
pyproject.toml
```

## Testing
- **pytest** for testing
- **pytest-cov** for coverage
- **hypothesis** for property-based testing
- Fixtures over setup/teardown

## Documentation (Google-style docstrings)

Use Google-style docstrings for public functions/classes.

```python
def normalize_date(input: str, *, time_zone: str) -> str:
    """Normalize a user-supplied date to an ISO string.

    Why:
        Storage and comparisons are safer when all dates are normalized.

    Args:
        input: User-supplied date (e.g. "2026-01-31").
        time_zone: IANA timezone (e.g. "America/Los_Angeles").

    Returns:
        ISO 8601 date string.

    Raises:
        ValueError: If the input cannot be parsed.
    """
    # ...
    raise NotImplementedError
```

Guidelines:
- Document inputs/outputs and error conditions.
- Prefer raising specific exceptions.

## Tools
- **Ruff**: Linting AND formatting (replaces flake8, isort, black)
- **mypy** or **pyright**: Type checking
- **uv** or **poetry**: Dependency management

```toml
# pyproject.toml
[tool.ruff]
line-length = 88
select = ["E", "F", "I", "N", "W", "UP", "ANN", "B", "C4", "SIM"]

[tool.mypy]
strict = true
```

## Style
- **4 spaces** indentation (PEP 8)
- **88 chars** line length (black/ruff default)
- **snake_case**: functions, variables, modules
- **PascalCase**: classes
- **SCREAMING_SNAKE_CASE**: constants

## Reference Docs
- PEP 8: https://pep8.org/
- Ruff Rules: https://docs.astral.sh/ruff/rules/
- mypy Docs: https://mypy.readthedocs.io/
- Python Type Hints: https://docs.python.org/3/library/typing.html
