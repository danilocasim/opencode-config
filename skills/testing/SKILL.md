---
name: testing
description: TDD-first testing playbook with stack routing (unit, integration, e2e)
---

# Testing Skill Index

Use this skill to produce reliable tests before implementation changes.

## When to load

- You are adding/changing behavior and need confidence.
- You are fixing a bug and need a repro test first.
- You need to choose a test framework or level for a stack.

## When NOT to load

- Work is pure docs/content with no behavior change.
- You only need static checks (lint/type/format) with no runtime behavior.

## Default policy (TDD-first)

- Red -> Green -> Refactor is default.
- Start at lowest layer that can prove behavior.
- Keep tests deterministic (no real network/time randomness without control).
- Assert outcomes, not implementation internals.
- Add regression test for every bug fix.

## Stack mapping

- Ruby/Rails -> `ruby-rails.md`
- Node/Next.js -> `node-nextjs.md`
- Python -> `python.md`
- Test docs/comment style -> `documentation-and-comments.md`
- Other stacks:
  - Go -> `go.md`
  - Rust -> `rust.md`
  - Swift -> `swift.md`
  - Kotlin -> `kotlin.md`

## Test levels

- Unit: pure logic, fast, isolated.
- Integration: DB/filesystem/process/API boundaries.
- End-to-end: full user workflows when necessary.

## Quick start checklist

- Identify behavior change in one sentence.
- Write failing test that proves the change.
- Implement minimal code to pass.
- Refactor with tests green.
- Update docs for public behavior changes.
