# Service and Query Objects

Use POROs to keep models/controllers thin: services handle workflows and side effects; queries handle read logic and filtering.

## When to load

- A use case spans multiple models, steps, or external systems.
- You need transaction boundaries, retries, or explicit failure handling.
- Query/filter logic is repeated across controllers/scopes/endpoints.

## When NOT to load

- Logic is a single model invariant or trivial finder.
- You are wrapping one line of code with no added contract.
- You need authorization rules (prefer dedicated policy objects).

## Core rules

- Service object = one business use case (`Namespace::Action.call(...)`).
- Query object = one read concern (`Namespace::Search.call(scope:, filters:)`).
- Define clear input/output contracts and failure semantics.
- Keep services orchestration-focused; move pure calculations to value objects.
- Use transactions explicitly where writes must be atomic.

## Common patterns

- `ApplicationService` base with class-level `.call`.
- Result contract (`success?`, `value`, `error`, optional `code`).
- Service names from domain verbs: `Orders::Checkout`, `Users::Invite`.
- Query objects returning `ActiveRecord::Relation` for composability/pagination.
- Parameter sanitizer for untrusted sort/filter input.

## Anti-patterns

- Service sprawl where every trivial method becomes a service.
- Query object that mutates records or triggers side effects.
- Services returning inconsistent shapes across success/failure paths.
- Rescuing everything without typed/domain errors.

## Checklist

- Is this truly a multi-step workflow or reusable read concern?
- Are inputs validated/sanitized at boundary entry?
- Is transaction scope explicit and minimal?
- Is output contract stable and documented?
- Are unit tests covering success, failure, and edge cases?

## References

- Active Record transactions: https://guides.rubyonrails.org/active_record_transactions.html
- ActiveSupport::Notifications: https://api.rubyonrails.org/classes/ActiveSupport/Notifications.html
