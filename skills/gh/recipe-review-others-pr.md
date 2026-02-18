# Recipe: Review and Comment on Others' PRs

Review someone else's PR efficiently: inspect changes, optionally run tests locally, draft your comments for confirmation, then post them with `gh`.

## Goal

Provide clear, actionable review feedback without losing context or missing important concerns.

## Load

- `SKILL.md`
- `prs.md`
- `../git/SKILL.md`

## Preconditions

- You have a PR number or URL.
- You have repository access to view/comment.

## Files to touch

- None unless you checkout locally to run tests.

## Steps

1. Collect PR context:

```bash
gh pr view <number> --json title,url,author,state,baseRefName,headRefName,reviewDecision,labels
gh pr diff <number>
```

2. Fetch PR conversation comments to avoid duplicating feedback:

```bash
gh pr view <number> --comments
```

3. Optional: checkout and run tests locally (recommended for risky changes):

```bash
gh pr checkout <number>
git status
<run project tests>
```

4. Draft your review notes in a confirmable list (do this before posting):

```text
Proposed PR comments:

1) <Severity: nit | suggestion | concern | blocking>
   <Comment text>

2) <Severity: ...>
   <Comment text>
```

5. Confirm with the user what to post:

```text
Post comments 1..N as:
- a single consolidated PR comment (recommended), or
- a review comment, or
- individual PR comments
```

6. Post comments (pick one style):

Single consolidated PR conversation comment (recommended for most reviews):

```bash
gh pr comment <number> -b "$(cat <<'EOF'
Review notes:

1) <comment>
2) <comment>

Optional:
- <praise for what is good>
- <risk/edge case to cover>
EOF
)"
```

Review comment (shows up as a review; does not approve/request-changes):

```bash
gh pr review <number> --comment -b "<your review text>"
```

Approve or request changes (only if you mean it):

```bash
gh pr review <number> --approve -b "LGTM"
gh pr review <number> --request-changes -b "Blocking: <reason>"
```

7. If you need to comment on a PR in another repo:

```bash
gh pr comment <number> -R owner/repo -b "<comment>"
```

## Anti-patterns

- Posting many tiny comments that could be one coherent note.
- Asking for changes without a reason and a suggested direction.
- Approving while also leaving a blocking comment.

## Test plan

- If you checked out locally: run the project test command(s) and mention them in your review.
- If you did not run tests: state that clearly.

## Commit message

(Not applicable - you are reviewing someone else's PR.)

## PR comment templates (copy-ready)

```text
Review notes:

1) (concern) <what could break>
   Suggestion: <concrete change>

2) (suggestion) <improvement>

3) (nit) <small style/readability>

Test notes:
- <tests you ran or didn't run>
```

```text
Blocking:
- <issue>

Why:
- <impact>

Suggested fix:
- <direction>
```
