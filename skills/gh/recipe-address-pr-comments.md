# Recipe: Address PR Comments (Your PR)

Address feedback on your pull request systematically: checkout branch, analyze comments, create an action plan, get user approval, implement changes, and reply to each comment thread.

## Goal

Turn PR feedback into either code changes or clear replies, with user approval at each step and proper threaded responses (not top-level comments).

## Load

- `SKILL.md`
- `prs.md`
- `../git/SKILL.md`
- Stack-specific skill based on PR changes (e.g., `../rails/SKILL.md`, `../nextjs/SKILL.md`)

## Preconditions

- You have a PR number or URL.
- You can push to the PR branch.

## Files to touch

- Your normal code files, plus tests if behavior changes.

## Steps

### 1. Switch to the PR branch

```bash
gh pr checkout <number>
git status
git log --oneline -3
```

### 2. Fetch all PR comments

**Conversation comments (general feedback):**

```bash
gh pr view <number> --comments
```

**Inline review/diff comments (line-level feedback):**

```bash
gh api repos/{owner}/{repo}/pulls/<number>/comments --jq '.[] | {id: .id, user: .user.login, path: .path, line: .line, body: .body, in_reply_to_id: .in_reply_to_id}'
```

### 3. Create a fix/change plan

Analyze each comment and categorize:

```text
PR Comment Action Plan
======================

Comment ID: 2820395876
File: src/components/UserProfile.tsx
Line: 45
Author: @reviewer
─────────────────────────────────────
Original comment:
"Consider extracting this validation logic into a separate hook"

Proposed action: [IMPLEMENT]
- Create useUserValidation hook
- Move validation logic from component
- Update component to use new hook
- Add tests for the hook

Estimated effort: 15 minutes
─────────────────────────────────────

Comment ID: 2820395880
File: src/utils/auth.ts
Line: 23
Author: @reviewer
─────────────────────────────────────
Original comment:
"This console.log should be removed before merge"

Proposed action: [IMPLEMENT]
- Remove console.log statement
- No tests needed (cleanup only)

Estimated effort: 2 minutes
─────────────────────────────────────

Comment ID: 2820395890
File: src/api/users.ts
Line: 67
Author: @reviewer
─────────────────────────────────────
Original comment:
"Should we add rate limiting here?"

Proposed action: [COMMENT]
- Reply explaining rate limiting is handled at middleware layer
- Point to existing rate limiter implementation

Reasoning: Out of scope for this PR, already covered
─────────────────────────────────────

Comment ID: 2820395900
File: src/components/Chart.tsx
Line: 34
Author: @reviewer
─────────────────────────────────────
Original comment:
"Consider using useMemo for expensive calculation"

Proposed action: [SKIP]
- Calculation is not expensive enough to warrant useMemo
- Benchmarked: 0.2ms average

Reasoning: Premature optimization, will add complexity without benefit
─────────────────────────────────────

SUMMARY:
- Implement: 2 comments
- Comment (reply only): 1 comment
- Skip: 1 comment
- Total estimated time: 20 minutes
```

### 4. Ask user for approval

Present the plan and ask for explicit direction:

```text
I've analyzed all PR comments and created an action plan.

**PROPOSED ACTIONS:**

✅ IMPLEMENT (2 comments):
   1. Extract validation hook (15 min)
   2. Remove console.log (2 min)

💬 COMMENT/REPLY (1 comment):
   3. Explain rate limiting is handled elsewhere

⏭️ SKIP (1 comment):
   4. useMemo suggestion (not needed - see reasoning)

**What would you like me to do?**

Options:
- "implement all" - Do all 2 implementations + replies
- "implement 1,2" - Only do specific items
- "skip 4" - Skip item 4, do the rest
- "comment on 3 only" - Just reply, no code changes
- "revise plan" - Let me know what to change

Please specify which items to implement, skip, or reply to.
```

### 5. Act on user's feedback

**For IMPLEMENT items:**

```bash
# Load relevant skills first
skill(name="rails")  # or nextjs, python, etc.
skill(name="testing")

# Make the changes
# ... implement fix ...

# Run tests if behavior changed
<run project test command>

# Stage and commit
git add -A
git commit -m "fix(<scope>): address PR feedback - <brief description>"
```

**For COMMENT items:**

Skip code changes, proceed to step 6 to reply.

**For SKIP items:**

No action needed, just note the reasoning for step 6 replies.

### 6. Create commits

Keep commits reviewable and focused:

```bash
# Review what changed
git status
git diff --stat

# If multiple logical changes, commit separately
git add src/components/UserProfile.tsx src/hooks/useUserValidation.ts
git commit -m "refactor(user): extract validation into useUserValidation hook

- Move validation logic from UserProfile component
- Add comprehensive tests for validation hook
- Addresses PR comment #2820395876"

git add src/utils/auth.ts
git commit -m "chore(auth): remove debug console.log

- Clean up leftover debug statement
- Addresses PR comment #2820395880"

# Push all commits
git push
```

### 7. Reply to comments (proper threaded replies, NOT top-level comments)

**IMPORTANT: Reply to each inline comment using the replies endpoint. Do NOT use top-level PR comments.**

For each comment you addressed, post a threaded reply:

```bash
# Reply to implemented changes
gh api repos/{owner}/{repo}/pulls/<number>/comments/<comment_id>/replies \
  -X POST \
  -f body='Fixed in commit <sha> - extracted validation into useUserValidation hook with tests'

# Reply to skipped items (explain why)
gh api repos/{owner}/{repo}/pulls/<number>/comments/<comment_id>/replies \
  -X POST \
  -f body='I looked into this, but the calculation averages 0.2ms in benchmarks. Adding useMemo would add complexity without meaningful performance benefit. Happy to revisit if we see performance issues in production.'

# Reply to acknowledged suggestions
gh api repos/{owner}/{repo}/pulls/<number>/comments/<comment_id>/replies \
  -X POST \
  -f body='Good point! Rate limiting is actually handled at the middleware layer (see src/middleware/rateLimiter.ts). This endpoint inherits that protection automatically.'
```

**Example with real values:**

```bash
gh api repos/beamtree/picq-web/pulls/2952/comments/2820395876/replies \
  -X POST \
  -f body='Fixed in commit 6c9284f91 - extracted validation into useUserValidation hook with comprehensive tests. The component is now much cleaner!'
```

**Why use the replies endpoint:**

- The `gh` CLI has no native command to reply to review comments (open feature request: cli/cli#11552)
- Top-level PR comments (`gh pr comment`) don't thread properly with review feedback
- The correct endpoint is `/pulls/<number>/comments/<comment_id>/replies` with POST method
- This creates proper threaded conversations that reviewers can see in context

### 8. Verify and summarize

```bash
# Check CI status
gh pr checks <number>

# View all your replies
gh api repos/{owner}/{repo}/pulls/<number>/comments --jq '.[] | select(.user.login == "<your-username>") | {id: .id, body: .body}'
```

**Post a summary comment (optional, only if helpful):**

Only post a top-level summary if there are multiple complex changes:

```bash
gh pr comment <number> -b "$(cat <<'EOF'
## Updates Made

### Implemented:
1. ✅ Extracted validation hook (commit: 6c9284f)
2. ✅ Removed debug console.log (commit: a3b2c1d)

### Replied:
3. 💬 Explained rate limiting architecture
4. 💬 Documented why useMemo wasn't needed (with benchmarks)

All CI checks passing. Ready for re-review!
EOF
)"
```

## Anti-patterns

- **Posting top-level comments** instead of threaded replies to review comments
- Replying "done" without pointing to what changed (commit SHA, files, or behavior)
- Making broad refactors while addressing narrow feedback
- Skipping tests when changing behavior
- Not getting user approval before implementing changes
- Combining multiple unrelated fixes into one commit
- Forgetting to reply to comments you skipped (always explain why)

## Test plan

- Run the repo test command(s) locally after each change
- Check `gh pr checks <number>` is green before finishing
- Verify threaded replies appear in the correct conversation threads

## Commit message templates

**For fixes:**

```
fix(<scope>): address PR feedback on <topic>

- <specific change made>
- <test updates if any>
- Addresses PR comment #<id>
```

**For refactors:**

```
refactor(<scope>): <description> per PR feedback

- <what changed and why>
- <impact>
- Addresses PR comment #<id>
```

**For cleanup:**

```
chore(<scope>): <cleanup task>

- <what was cleaned up>
- Addresses PR comment #<id>
```

## Reply templates (for threaded comments)

**Implemented:**

```text
Fixed in commit <sha>:
- <what changed>
- <test coverage>
```

**Acknowledged with explanation:**

```text
Good catch! I looked into this and <explanation of what you found>.

<why you're not changing it / what you did instead>
```

**Out of scope (with context):**

```text
This is a great suggestion but out of scope for this PR because <reason>.

<where it should be handled instead>

Happy to create a follow-up issue if you'd like!
```

**Question for clarification:**

```text
I'm not sure I understand the suggestion. Are you asking for:
- <option A>, or
- <option B>?

Could you clarify what you'd like to see here?
```
