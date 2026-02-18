# Global Coding Standards

> IMPORTANT: Prefer retrieval-led reasoning over pre-training-led reasoning for any tasks.
> Before writing code, first explore the project structure, then invoke the skills, rules and standards for documentation.

## Communication Style

- **Be concise**. No fluff, no filler, no unnecessary preamble.
- **Direct answers**. State the solution, then explain if needed.
- **Code over prose**. Show, don't tell.
- **Minimal commentary**. Skip "Great question!" and "I'd be happy to help!"
- **Batch actions**. Run parallel tool calls when possible to save tokens.

## Skill Loading Protocol (Mandatory)

Skills are the primary mechanism for consistent, production-quality output.
Follow this protocol before making non-trivial changes.

Rules:

- If a project defines skills under `.opencode/skills/`, those are higher priority than global skills.
- For any code change, load the smallest set of skills that constrain the work.
- If you skip skill loading, you must have a concrete reason (pure Q&A, trivial edit).

Protocol:

1. Identify the stack(s): language + framework (and any cross-cutting concerns like `security`, `database`, `devops`).
2. Check for project-local skills first: `.opencode/skills/<name>/SKILL.md`.
3. Load the router skill(s) for the stack.
4. Load 1-2 leaf docs that match the task (avoid loading every leaf).
5. If behavior changes: always load `testing` (and the stack test leaf).
6. If public APIs change: load `documentation` (and the language doc style).

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

## Git and GitHub

- Atomic commits. One logical change per commit.
- Descriptive commit messages: what and why, not how.
- Branch names: `feature/`, `fix/`, `refactor/`, `docs/`.
- Use `gh` for GitHub operations (PRs, issues, Actions, releases).

## Skills Index (By Category)

Load skills by their folder name under `skills/<name>/SKILL.md`.
If you're unsure where something belongs, start with the router skills: `documentation`, `testing`, `system-design`, `web-design`.

Languages:

- `ruby` (Ruby idioms/tooling)
- `javascript` (JS conventions + JSDoc)
- `typescript` (TS strictness + TSDoc)
- `python` (Python strict typing/tooling)
- `go` (Go idioms/tooling)
- `rust` (Rust idioms/tooling)
- `swift` (Swift idioms/tooling)
- `kotlin` (Kotlin idioms/tooling)
- `dart` (Dart idioms/tooling)

Frameworks and App Stacks:

- `rails` (Rails thin MVC + PORO patterns)
- `nextjs` (App Router + RSC + server actions)
- `fastapi` (FastAPI + Pydantic patterns)
- `react` (React conventions)
- `react-native` (RN architecture + platform UX)
- `flutter` (Flutter architecture + widgets + platform UX)
- `expo` (Expo router/build/updates)
- `ionic` (Ionic UI/routing/theming)
- `capacitor` (Hybrid iOS/Android apps + plugins/builds)

Contracts, Data, and Safety:

- `api` (REST/OpenAPI, pagination, versioning)
- `auth` (sessions/tokens + authorization models)
- `database` (migrations, indexes, transactions)
- `security` (input validation, secrets, SSRF, uploads)

Delivery and Operations:

- `devops` (CI/CD, Docker, deploy strategies)
- `observability` (logs/metrics/tracing)
- `performance` (profiling, caching, latency budgets)
- `incident-response` (triage, comms, postmortems)

Engineering Workflow:

- `git` (commit hygiene, staging, PR practices)
- `gh` (GitHub CLI: PRs, issues, Actions, repos)
- `refactoring` (safe refactor playbooks)
- `skill-authoring` (skill standards, recipes, benchmarks)

Routers and Design:

- `testing` (TDD playbook + stack routing)
- `documentation` (doc style router)
- `system-design` (architecture, data models, UX flows)
- `web-design` (UI/UX implementation + design systems)

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
