# Data Fetching, Cache, and Revalidation

Most stale-data bugs come from unclear cache ownership. Define fetch intent up front: static, dynamic, or revalidated.

## When to load

- Implementing or debugging server-side data fetching.
- Choosing cache mode and revalidation strategy.
- Designing invalidation after writes.

## When NOT to load

- You only need component hierarchy guidance (`atomic-components.md`).
- You only need mutation implementation details (`server-actions-and-mutations.md`).

## Core rules

- Prefer server-side fetching in Server Components.
- Pick one intent per query: `force-cache`, `no-store`, or `revalidate`.
- Use domain tags for invalidation (`projects`, `project:{id}`).
- Keep read and write paths aligned on same tag/path invalidation keys.

## Common patterns

- `next: { revalidate: 60 }` for freshness windows.
- `revalidateTag` for domain-scoped invalidation.
- `revalidatePath` for route-scoped refresh where coupling is acceptable.

## Anti-patterns

- Blanket `no-store` everywhere.
- Mixed conflicting cache strategies with no intent.
- Broad path revalidation for narrow data changes.

## Checklist

- Is cache intent explicit for each critical fetch?
- Do write paths invalidate the exact read tags/paths?
- Is invalidation colocated with mutation logic?

## References

- Next.js data fetching: https://nextjs.org/docs/app/building-your-application/data-fetching
- Caching and revalidation: https://nextjs.org/docs/app/building-your-application/caching
