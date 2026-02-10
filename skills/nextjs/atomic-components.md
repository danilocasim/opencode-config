# Atomic Components in Next.js (Hybrid)

Pure atomic design is often too rigid for product work. Hybrid atomic keeps a clean design system while preserving feature ownership.

## When to load

- Defining component taxonomy (atom/molecule/organism/template).
- Deciding shared vs feature-local component placement.
- Reviewing component reuse and abstraction quality.

## When NOT to load

- Task is route/layout boundaries (`app-router-and-rsc-boundaries.md`).
- Task is cache/revalidation behavior (`data-fetching-cache-and-revalidation.md`).
- Task is mutation flow (`server-actions-and-mutations.md`).

## Core rules

- Shared primitives (`components/ui`) are stable and domain-neutral.
- Composites default to feature-local unless reused by 2+ features.
- Route-level templates belong in `app/*`.
- Keep domain terms in feature-local component names.

## Common patterns

- `Button`, `Input`, `Dialog` in shared `components/ui`.
- `InvoiceStatusPill`, `ProjectMemberRow` in feature folders.
- Promote to shared only when API can stay domain-neutral.

## Anti-patterns

- Moving domain-specific components into shared `ui` too early.
- Creating deep global atomic hierarchies no feature owns.
- Reusable component names that leak product-specific assumptions.

## Checklist

- Is this component domain-neutral and reused enough to be shared?
- If not, is it kept under `features/<feature>/components`?
- Does naming communicate ownership and intent?

## References

- Atomic Design: https://atomicdesign.bradfrost.com/
- Next.js docs: https://nextjs.org/docs
