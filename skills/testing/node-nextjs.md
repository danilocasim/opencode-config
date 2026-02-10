# Node / Next.js Testing (TDD-First)

Use this guide for Node backends, shared TS/JS libs, and Next.js apps.

## When to load

- You are testing Node/Next.js logic, routes, server actions, or UI components.
- You need clear test-level routing (unit vs integration vs e2e).

## When NOT to load

- Non-JS stacks.
- Pure lint/type tasks.

## Core rules

- Use existing repo tools: Vitest preferred for new setups, Jest if already present.
- React UI tests: React Testing Library + user-event.
- API/network isolation: MSW where HTTP mocking is needed.
- E2E: Playwright for critical workflows only.

## Common patterns

- Unit tests for pure `lib` logic and validators.
- Integration tests for route handlers and server actions.
- Component tests assert user-visible behavior and accessibility.
- E2E for auth, checkout, and other business-critical paths.

```ts
import { describe, expect, it } from "vitest";

describe("normalizeSlug", () => {
  it("lowercases and replaces spaces", () => {
    expect(normalizeSlug("Hello World")).toBe("hello-world");
  });
});
```

## Anti-patterns

- Snapshot-heavy tests for business logic.
- Mocking framework internals instead of user outcomes.
- E2E-first for behavior that unit/integration can prove.
- Real network calls in CI unit tests.

## Checklist

- Is test level the smallest that proves behavior?
- Are auth/error paths covered for routes/actions?
- Are network/time sources controlled?
- Are critical flows covered in Playwright without over-expanding suite size?

## References

- Vitest: https://vitest.dev/
- React Testing Library: https://testing-library.com/docs/react-testing-library/intro/
- Playwright: https://playwright.dev/
