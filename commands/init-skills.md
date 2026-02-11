---
description: Bootstrap project-local skills from the repo (project skill)
agent: build
---

Bootstrap project-local skills for this repo under `.opencode/skills/`.

Goals:

- Create a `project` skill router that captures repo-specific conventions.
- Prefer observation over guesswork: read files to detect stack and commands.
- Keep the skill small and high-signal.
- Do not overwrite existing `.opencode/skills/project/*` files without warning.

Process:

1. Detect the stack by checking for common files:
   - JavaScript/TypeScript: `package.json`, `pnpm-lock.yaml`, `bun.lockb`
   - Ruby/Rails: `Gemfile`, `Gemfile.lock`
   - Python: `pyproject.toml`, `requirements.txt`
   - Go: `go.mod`
   - Rust: `Cargo.toml`
   - Flutter/Dart: `pubspec.yaml`
2. Extract developer commands:
   - from `package.json` scripts, Makefile targets, or README
3. Create:
   - `.opencode/skills/project/SKILL.md` (router)
   - `.opencode/skills/project/conventions.md` (leaf)
4. Include in `conventions.md`:
   - how to run format/lint/test/build
   - directory ownership conventions (where features live)
   - environment notes (required versions, local services)
   - a short "load order" note: load `project` first, then global routers
5. Run skills lint against project-local skills:
   - `python3 $HOME/.config/opencode/scripts/skills_lint.py --skills-dir .opencode/skills`

Output:

- List the created files and summarize the detected stack + commands.
