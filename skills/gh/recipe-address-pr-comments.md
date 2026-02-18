# Recipe: Address PR Comments (Your PR)

Address feedback on your pull request quickly: fetch comments, decide what needs code changes, push updates, and reply.

## Goal

Turn PR feedback into either code changes or clear replies, with minimal back-and-forth.

## Load

- `SKILL.md`
- `prs.md`
- `../git/SKILL.md`

## Preconditions

- You have a PR number or URL.
- You can push to the PR branch.

## Files to touch

- Your normal code files, plus tests if behavior changes.

## Steps

1. Identify the PR and repo context:

```bash
gh pr view <number> --json number,title,url,headRefName,baseRefName
```

2. Fetch PR conversation comments (high signal for general feedback):

```bash
gh pr view <number> --comments
```

3. Fetch inline review/diff comments (line-level feedback):

```bash
gh api repos/{owner}/{repo}/pulls/<number>/comments --jq '.[] | {id: .id, user: .user.login, path: .path, line: .line, body: .body}'
```

4. Build an "action list" from comments (use this format so it is easy to respond):

```text
[ ] <comment id or link>: <short restatement> -> (change | explain)
```

5. Checkout the PR branch (if you are not already on it):

```bash
gh pr checkout <number>
git status
```

6. For each action item:

```text
If change:
- implement fix
- add/update tests if behavior changes
- run the project's test command(s)

If explain:
- write a short, specific reply (why no change; what you verified)
```

7. Commit and push changes (repeat as needed; keep commits reviewable):

```bash
git status
git diff
git add -A
git commit -m "<message>"
git push
```

8. Reply back on the PR:

Conversation reply (general):

```bash
gh pr comment <number> -b "<reply with what changed + commit SHA(s) or reasoning>"
```

Reply to a specific inline review comment (threaded):

1. Get the comment ID from step 3 output (the `id` field)
2. Use the replies endpoint (requires PR number in path):

```bash
gh api repos/{owner}/{repo}/pulls/<number>/comments/<comment_id>/replies \
  -X POST \
  -f body='<your reply message>'
```

Example:

```bash
gh api repos/beamtree/picq-web/pulls/2952/comments/2820395876/replies \
  -X POST \
  -f body='Fixed in commit 6c9284f91 - removed the nil checks as suggested'
```

**Why this approach:**

- The `gh` CLI has no native command to reply to review comments (open feature request: cli/cli#11552)
- The previous endpoint `/pulls/<number>/comments` with `in_reply_to` parameter doesn't work
- The correct endpoint is `/pulls/<number>/comments/<comment_id>/replies` with POST method
- The PR number is required in the URL path, not just the comment_id

9. Verify CI status (optional but recommended):

```bash
gh pr checks <number>
```

## Anti-patterns

- Replying "done" without pointing to what changed (commit SHA, files, or behavior).
- Making broad refactors while addressing narrow feedback.
- Skipping tests when changing behavior.

## Test plan

- Run the repo test command(s) locally.
- Check `gh pr checks <number>` is green.

## Commit message

- `fix(<scope>): address PR feedback on <topic>`

## PR replies (copy-ready)

```text
Addressed in <sha>:
- <what changed>

Verified:
- <tests run>

Notes:
- <why this approach / why no change for some items>
```

```text
I don't think we need to change this because:
- <reason>

Verified:
- <what you checked>
```
