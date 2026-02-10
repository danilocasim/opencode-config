# TypeScript/JavaScript Testing (Vitest/Jest)

If you are testing a Next.js app (App Router, server actions, route handlers), prefer `node-nextjs.md`.

## Defaults

- Prefer Vitest for new projects; use Jest if the repo already uses it
- Prefer behavior-focused tests with clear assertions

## Unit tests (Vitest)

```ts
import { describe, expect, it } from "vitest";

import { normalizeDate } from "./normalizeDate";

describe("normalizeDate", () => {
  it("returns ISO date", () => {
    expect(normalizeDate("2026-01-31", "UTC")).toBe("2026-01-31");
  });
});
```

## React component tests (RTL)

- Use `@testing-library/react` + `@testing-library/user-event`
- Assert what the user can see and do

```tsx
import { render, screen } from "@testing-library/react";
import userEvent from "@testing-library/user-event";

import { Counter } from "./Counter";

it("increments when clicked", async () => {
  const user = userEvent.setup();
  render(<Counter />);
  await user.click(screen.getByRole("button", { name: /count/i }));
  expect(screen.getByText(/count: 1/i)).toBeInTheDocument();
});
```

## Network isolation

- Prefer MSW (Mock Service Worker) for HTTP mocking when appropriate
