---
name: database
description: Database patterns for migrations, indexing, transactions, and performance
---

# Database Conventions

## Migrations

- Always use migrations for schema changes
- Backfill data in safe batches
- Avoid long-running locks in production

## Indexing

- Index by query patterns
- Watch for N+1 queries

## Transactions

- Use transactions for multi-step invariants
- Keep transaction scope small

## Safety

- Validate inputs
- Use parameterized queries
