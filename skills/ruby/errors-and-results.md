# Ruby Errors and Results

## When to load

- You are defining failure behavior for domain or integration boundaries.
- You need consistency between exceptions and explicit result objects.

## When NOT to load

- The change is only formatting or naming.
- The main task is dependency/tooling setup.

## Core rules

- Raise specific exception classes for exceptional conditions.
- Include actionable context in error messages.
- Reserve broad rescue for process boundaries, not core logic.
- Use result objects when failure is expected and part of normal flow.

## Patterns

- Custom error hierarchy per domain area.
- `raise NewError, message, cause:` or `raise NewError.new(...)` with cause.
- `Result = Data.define(:ok?, :value, :error)` style for expected outcomes.
- Map low-level errors to domain errors at boundaries.

## Anti-patterns

- `rescue StandardError` inside deep domain code.
- Swallowing exceptions and returning `nil` silently.
- Mixing result objects and exceptions in the same API without contract docs.

## Checklist

- Failure contract is documented and predictable.
- Callers can handle error paths without guessing.
- Unexpected errors still surface with useful context.

## References

- https://docs.ruby-lang.org/en/master/Exception.html
- https://www.honeybadger.io/blog/ruby-exception-vs-standarderror-whats-the-difference/
- https://rubystyle.guide/#exception-class-messages
