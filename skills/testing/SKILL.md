---
name: testing
description: Test strategy and framework index by language (unit, integration, e2e)
---

# Testing Skill Index

This skill routes test-writing to the correct framework conventions.

## Defaults

- Prefer tests that prevent regressions (bug repro -> red -> fix -> green)
- Keep tests deterministic (no time, network, randomness without control)
- Prefer unit tests; use integration tests at boundaries

## Language mapping

- Python: pytest
  - See: `skills/testing/python.md`
- TypeScript/JavaScript: Vitest or Jest
  - See: `skills/testing/typescript.md`
- React UI tests: React Testing Library + user-event
  - See: `skills/testing/typescript.md`
- Ruby/Rails: RSpec (or Minitest if project uses it)
  - See: `skills/testing/ruby.md`
- Go: standard library `testing` + table tests
  - See: `skills/testing/go.md`
- Rust: `#[test]` + integration tests in `tests/`
  - See: `skills/testing/rust.md`
- Swift: XCTest
  - See: `skills/testing/swift.md`
- Kotlin: JUnit 5 + MockK
  - See: `skills/testing/kotlin.md`

## Test levels

- Unit: pure logic, fast, isolated
- Integration: DB/filesystem/process boundaries
- End-to-end: full system flows (browser/API) when needed

## What good tests include

- Clear naming (behavior focused)
- Edge cases and error paths
- Minimal setup with helpers/fixtures
- Assertions on outcomes, not implementation
