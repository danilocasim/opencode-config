---
description: Run the closest equivalent of CI locally
agent: build
---

Run the project's CI-like checks.

$ARGUMENTS

Workflow:
1. Identify the CI entrypoint (package.json scripts, Makefile, GitHub Actions, etc.).
2. Run format/lint/tests/build in the same order.
3. Summarize failures and fix the highest-signal issues first.
