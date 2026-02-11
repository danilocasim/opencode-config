---
name: database
description: Database patterns for migrations, indexing, transactions, and performance
---

# Database Skill Router

Use this skill when schema, query patterns, or transactional boundaries matter. The goal is correctness first, then performance, without risky production operations.

## When to load

- You are writing a migration/backfill.
- You are adding indexes or changing query patterns.
- You need a transaction boundary for multi-step invariants.
- You are debugging slow queries or N+1 behavior.

## When NOT to load

- You are designing API contracts (use `../api/SKILL.md`).
- You are doing framework-only refactors without DB behavior changes.

## Routing table

| If the task is about...                        | Load file                           |
| ---------------------------------------------- | ----------------------------------- |
| Safe migrations and data backfills             | `migrations-and-backfills.md`       |
| Indexing by query patterns                     | `indexes-and-query-patterns.md`     |
| Transaction boundaries and consistency         | `transactions-and-consistency.md`   |
| Query performance and avoiding N+1             | `query-performance-and-n-plus-1.md` |
| Recipe: online schema change (expand/contract) | `recipes-online-migration.md`       |

## Typical load combos

- New column rollout: `migrations-and-backfills.md` + `recipes-online-migration.md`
- Slow endpoint: `query-performance-and-n-plus-1.md` + `indexes-and-query-patterns.md`
