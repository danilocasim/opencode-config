# Migrations and Backfills

Schema changes are easy to write and hard to run in production. Optimize for safety: short locks, resumable backfills, and deployable sequences.

## When to load

- You are changing schema on a production table.
- You need to backfill existing rows.
- You want a safe rollout plan (expand -> backfill -> contract).

## When NOT to load

- You only need indexing rules (`indexes-and-query-patterns.md`).
- You only need transaction boundaries (`transactions-and-consistency.md`).

## Core rules

- Prefer expand/contract.
- Keep migrations fast; avoid running large data updates inside a deploy-time migration.
- Backfills should be resumable (cursor/batches) and bounded.
- Avoid table rewrites on big tables (type changes, defaults that rewrite).
- Add constraints only after data is clean.

## Minimal examples

Expand (fast):

```sql
ALTER TABLE users ADD COLUMN normalized_email text;
```

Backfill in batches (pseudo):

```text
for id range in batches:
  update rows set normalized_email = lower(trim(email))
  record progress
```

Contract (later):

```sql
ALTER TABLE users ALTER COLUMN normalized_email SET NOT NULL;
```

## Anti-patterns

- Backfilling millions of rows inside a migration.
- Unbounded “one shot” scripts with no resume point.
- Adding NOT NULL constraints before backfill.

## Checklist

- Expand/contract plan written down.
- Backfill is batched and resumable.
- Risky operations avoided (table rewrite, long locks).
- Constraints added only after data is valid.
