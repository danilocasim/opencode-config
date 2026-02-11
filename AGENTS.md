# Global Coding Standards

> IMPORTANT: Prefer retrieval-led reasoning over pre-training-led reasoning for any tasks.
> Before writing code, first explore the project structure, then invoke the skills, rules and standards for documentation.

## Communication Style

- **Be concise**. No fluff, no filler, no unnecessary preamble.
- **Direct answers**. State the solution, then explain if needed.
- **Code over prose**. Show, don't tell.
- **Minimal commentary**. Skip "Great question!" and "I'd be happy to help!"
- **Batch actions**. Run parallel tool calls when possible to save tokens.

## Philosophy

- **Minimal & Concise**: Less code is better. If it can be shorter, make it shorter.
- **No Over-Engineering**: Write code a newbie can understand. Simple > clever.
- **DRY**: Never repeat yourself unless it's truly a one-off.
- **Best Path**: Find the right solution, don't monkey-patch.

## Code Structure

- **Max 250 lines per file**. Always find a way to extract or refactor.
- **Section code with blank lines** for visual clarity.
- **Partition logically**: group related functions, separate concerns.

Note: For agent/skill/config prompt files (this repo), longer files are acceptable when it improves retrieval and reuse. Prefer splitting only when it helps indexing.

## Testing (TDD)

- **Red/Green/Refactor**: Write failing test first, make it pass, then refactor.
- Always run tests after changes. Fix failures immediately.
- Prefer unit tests. Integration tests for boundaries.
- Test edge cases and error paths.
- Use **Playwright** for browser automation and end-to-end testing when possible.

## Documentation

- **Document heavily**. Every public function/method needs a docstring.
- Explain WHY, not just WHAT.
- Update docs when changing behavior.
- Use language-idiomatic doc formats (defined in each `skills/<language>/SKILL.md`).

## Type Safety

- Use strict typing. Enable strictest compiler/linter settings.
- Explicit error handling. No silent failures.
- Validate inputs at boundaries.

## Git

- Atomic commits. One logical change per commit.
- Descriptive commit messages: what and why, not how.
- Branch names: `feature/`, `fix/`, `refactor/`, `docs/`.

## Language-Specific Conventions

When working in a specific language, load the appropriate skill for detailed conventions:

- **Ruby**: Load `ruby` skill for Ruby 3.x idioms and Rubocop rules
- **JavaScript**: Load `javascript` skill for JS conventions and JSDoc
- **TypeScript**: Load `typescript` skill for TS 5.x strict patterns and TSDoc
- **Python**: Load `python` skill for Python 3.12+ and Ruff/Pyright rules
- **Rust**: Load `rust` skill for idiomatic Rust and Clippy lints
- **Go**: Load `go` skill for Go conventions, GoDoc, and table-driven tests
- **Swift**: Load `swift` skill for Swift conventions and SwiftDoc
- **Kotlin**: Load `kotlin` skill for Kotlin conventions and KDoc
- **DevOps**: Load `devops` skill for Docker/CI/infrastructure patterns
- **Dart**: Load `dart` skill for Dart 3.x idioms, null safety, and tooling
- **Flutter**: Load `flutter` skill for Flutter architecture, widgets, and platform UX
- **Capacitor**: Load `capacitor` skill for production iOS/Android hybrid apps and native build workflows
- **Ionic**: Load `ionic` skill for Ionic UI, routing, theming, and Capacitor integration

## Routing Skills

- For documentation style selection, load `documentation` (routes to YARD/JSDoc/TSDoc/docstrings/etc.).
- For test framework selection, load `testing` (routes to pytest/Vitest/Jest/RSpec/etc.).
- For system design work, load `system-design` (architecture patterns, data modeling, API design, UX flows, UI specs).
- For UI/UX implementation, load `web-design` (routes to component skills, Tailwind, shadcn patterns).

## Skills Index

Load these by name (they route you to the right leaf docs):

- **api**: REST/OpenAPI conventions, error contracts, pagination, versioning
- **auth**: Sessions/tokens and authorization models with safe defaults
- **capacitor**: Production hybrid iOS/Android apps, plugins, builds, WebView UX
- **database**: Migrations/backfills, indexing, transactions, query performance
- **dart**: Dart 3.x null safety, async/streams, tooling, testing
- **devops**: Docker, CI pipelines, secrets in CI, deploy strategies
- **documentation**: Doc style router (YARD/JSDoc/TSDoc/docstrings)
- **expo**: Expo Router, EAS build/dev client, updates, capabilities
- **fastapi**: FastAPI conventions with Pydantic
- **flutter**: Flutter architecture, widgets/theming, platform UX, testing
- **git**: Commit hygiene, staging, PR practices
- **incident-response**: Triage/mitigation, comms, postmortems
- **ionic**: Ionic UI/routing/theming + Capacitor integration
- **javascript**: JS conventions + JSDoc
- **kotlin**: Kotlin conventions + KDoc
- **nextjs**: App Router + RSC boundaries, data/cache, server actions
- **observability**: Logs/metrics/tracing + production debugging playbooks
- **performance**: Profiling discipline, caching, latency budgets
- **python**: Python 3.12+ strict typing/tooling router
- **rails**: Thin MVC Rails, services/queries, concerns, tests
- **react**: React (TS) conventions for web apps
- **react-native**: React Native architecture, platform UX, native integration
- **refactoring**: Safe refactor workflows and extraction playbooks
- **ruby**: Ruby 3.x idioms, tooling, and design
- **rust**: Rust conventions and idioms
- **security**: Input validation, secrets, web threats, SSRF, uploads
- **skill-authoring**: Skill routers/leaf standards, recipes, benchmarks
- **swift**: Swift conventions and SwiftDoc
- **system-design**: Architecture, data modeling, APIs, UX flows
- **testing**: TDD playbook + stack routing, E2E, mocks, CI reliability
- **typescript**: TS 5.x strict type safety + TSDoc
- **web-design**: UI/UX implementation patterns, design systems, components

These skills contain modern conventions (2024-2026), tooling configs, and reference docs.

## When Exploring Code

- Read existing patterns before writing new code.
- Match the codebase style, even if you disagree.
- Ask about conventions if unsure.

## When Uncertain

- Ask clarifying questions before implementing.
- Present options with tradeoffs when multiple approaches exist.
- Prefer reversible decisions over irreversible ones.

## Project Context Priority

1. **Project AGENTS.md / rules** - highest priority
2. **Project conventions** - inferred from existing code
3. **Global skills** - language-specific knowledge
4. **Global AGENTS.md** - these defaults (lowest priority)

Always defer to project-specific rules when they exist.
