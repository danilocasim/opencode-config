---
description: Review code for quality, DRY violations, and best practices
agent: code-reviewer
subtask: true
---

Review the following code for quality issues:

$ARGUMENTS

Focus on:

1. Simplicity - could this be simpler?
2. DRY violations - any repeated logic?
3. Documentation - are public APIs documented?
4. Type safety - explicit types, proper error handling?
5. Data access - any N+1 DB calls, query-in-loop patterns, or chatty I/O?
6. Correctness at boundaries - null/error states, transactions, race conditions?
7. Security basics - auth/authz gaps, input validation, sensitive data exposure?
8. Concurrency/idempotency - duplicate writes, retry safety, race-prone flows?
9. API and migration safety - contract drift, unsafe schema/data rollout?
10. File length - is it under 250 lines?

Provide specific, actionable feedback.
