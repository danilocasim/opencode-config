# OpenCode Config + Skill Library

This repo is a personal/team OpenCode configuration and a "router-first" skills library.
The goal is to make LLM coding behavior predictable, production-quality, and easy to reuse across projects.

If you are reading this in `~/.config/opencode`, OpenCode will automatically discover:

- `opencode.json` (global config)
- `AGENTS.md` (global rules injected into context)
- `skills/*/SKILL.md` (global skills)
- `commands/*.md` (custom commands)
- `scripts/*` (QA utilities)
- `templates/*` (copy into projects)

## How OpenCode Uses This Repo

OpenCode pulls behavior from a few sources:

- Rules: `AGENTS.md` (plus `instructions/*` referenced by `opencode.json`)
- Skills: global `skills/<name>/SKILL.md` and project-local `.opencode/skills/<name>/SKILL.md`
- Commands: global `commands/*.md` and project-local `.opencode/commands/*.md`
- Plugins/tools: global `plugins/*` and project-local `.opencode/plugins/*` / `.opencode/tools/*`

Project-local always wins for repo-specific conventions.

## Skill-First Workflow

This repo is built around one idea: skills are the primary mechanism for consistent output.

The enforced workflow is:

1. Identify the stack (language + framework) and cross-cutting concerns (`security`, `database`, `devops`).
2. Check project-local skills first: `.opencode/skills/*`.
3. Load the router skill(s) for the stack.
4. Load 1-2 relevant leaf docs.
5. If behavior changes: load `testing` (+ the stack test leaf).
6. If public APIs change: load `documentation` (+ language doc style).

Use the `/skills` command (see `commands/skills.md`) as the runbook.

## Recommended Per-Project Setup

For any repo you care about, add project-local guidance so the agent can follow your conventions.

### 1) Bootstrap a project-local `project` skill

Use the command:

- `/init-skills` (see `commands/init-skills.md`)

This creates:

- `.opencode/skills/project/SKILL.md`
- `.opencode/skills/project/conventions.md`

That `project` router should encode what global skills cannot know:

- where features live
- how to run format/lint/test/build
- required runtimes and local services
- what "good" looks like in this repo

### 2) Enforce skill loading before edits (SkillGuard)

If you want hard guardrails, install a project-local plugin:

- `/init-skill-guard` (see `commands/init-skill-guard.md`)

This installs a plugin under `.opencode/plugins/` that blocks file modifications until skills are loaded.

Templates:

- `templates/project-local-plugins` (SkillGuard and the stricter ProjectSkillGuard)
- `templates/project-local-skills` (starter local skill tree)

## QA and Regression Checks

This repo ships two linters:

- Skills lint: `python3 scripts/skills_lint.py`
- Benchmarks lint: `python3 scripts/benchmarks_lint.py`

Baseline "CI-like" checks for this repo:

```bash
python3 scripts/skills_lint.py
python3 scripts/benchmarks_lint.py
npx prettier --check .
```

See `commands/ci.md`.

## Authoring Skills (Repo Standards)

Skills are router-first:

- Every skill has `skills/<name>/SKILL.md` with a routing table.
- Leaf docs stay narrow: decision rules, checklists, anti-patterns, and 1-3 canonical examples.

See `skills/skill-authoring/SKILL.md`.

## Notes

- Commands in `commands/*.md` are auto-discovered by OpenCode (no `opencode.json` wiring required).
- Skills are loaded on-demand via the `skill` tool; they do not auto-load unless the agent is instructed or forced by guardrails.
- For team use, commit project-local `.opencode/skills/` (and optionally `.opencode/plugins/`) to each repo.
