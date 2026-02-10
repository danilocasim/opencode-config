# Ruby Objects and Design

## When to load

- You are deciding where behavior should live across classes/modules.
- You are extracting business logic from scripts/controllers into POROs.

## When NOT to load

- The task is mostly syntax/style cleanup.
- The main concern is test tooling or CI configuration.

## Core rules

- Prefer composition over inheritance.
- Keep objects focused on one reason to change.
- Expose small public APIs and keep collaborators explicit.
- Isolate side effects (I/O, DB, HTTP) behind boundaries.

## Patterns

- Service object for one business action (`call`/`run`).
- Query object for reusable filtering/search logic.
- Value object for domain primitives (money, email, date range).
- Policy object for authorization decisions.

## Anti-patterns

- God objects with mixed persistence, orchestration, and formatting.
- Inheritance trees for behavior that could be collaborator-based.
- Hidden dependencies via constants/globals.

## Checklist

- Object name reflects one business concept.
- Constructor dependencies are explicit and minimal.
- Public methods are small, stable, and testable in isolation.

## References

- https://sandimetz.com/99bottles
- https://rubystyle.guide/
- https://martinfowler.com/eaaCatalog/
