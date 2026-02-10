---
description: Lint ~/.config/opencode/skills for consistency
agent: build
---

Run the global skills linter and fix any issues.

Here is the current lint output:

!`python3 ~/.config/opencode/scripts/skills_lint.py`

If there are errors:

- Identify the failing file(s)
- Apply minimal fixes to satisfy required headings / frontmatter
- Re-run the linter until it passes
