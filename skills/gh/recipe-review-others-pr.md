# Recipe: Review and Comment on Others' PRs

Review someone else's PR with proper inline comments: inspect changes, load relevant skills, draft review comments for approval, then post them as a proper review with threaded feedback.

## Goal

Provide clear, actionable review feedback using GitHub's review system (not top-level comments), with proper line references and code suggestions.

## Load

- `SKILL.md`
- `prs.md`
- `../git/SKILL.md`
- `../code-reviewer/SKILL.md` (for review quality)
- Stack-specific skill (e.g., `../rails/SKILL.md`, `../nextjs/SKILL.md`) based on PR changes

## Preconditions

- You have a PR number or URL.
- You have repository access to view/comment.

## Files to touch

- None (review only, unless you need to checkout to understand context).

## Steps

1. **Collect PR context:**

```bash
gh pr view <number> --json title,url,author,state,baseRefName,headRefName,reviewDecision,labels,body
```

2. **Inspect the diff to understand changes:**

```bash
gh pr diff <number>
```

3. **Load necessary skills based on the code being reviewed:**

Identify the stack from file extensions and paths:

- `.rb` files + `Gemfile` → Load `rails/SKILL.md` + `ruby/SKILL.md`
- `.tsx/.ts` files + `package.json` → Load `nextjs/SKILL.md` or `react/SKILL.md`
- `.py` files → Load `python/SKILL.md` + `fastapi/SKILL.md` if applicable
- Database migrations → Load `database/SKILL.md`
- API changes → Load `api/SKILL.md`
- Security-sensitive code → Load `security/SKILL.md`

4. **Fetch existing review comments to avoid duplication:**

```bash
gh api repos/{owner}/{repo}/pulls/<number>/comments --jq '.[] | {id: .id, user: .user.login, path: .path, line: .line, body: .body}'
```

5. **Checkout the PR branch (optional but recommended for complex reviews):**

```bash
gh pr checkout <number>
git log --oneline origin/<base>..HEAD
```

6. **Draft your review comments in a confirmable list:**

Present to user for approval before posting:

````text
Proposed PR Review Comments:

File: src/components/UserProfile.tsx
─────────────────────────────────────
Line 45-52 (start_line: 45, line: 52):
Severity: [suggestion]
Comment: Consider extracting this validation logic into a separate hook

```typescript
// Suggested change:
const useUserValidation = (user: User) => {
  const errors = [];
  if (!user.email) errors.push('Email required');
  if (!user.name) errors.push('Name required');
  return errors;
};
````

Reasoning: This would make the component cleaner and allow reuse in other forms.

─────────────────────────────────────

File: src/utils/auth.ts
─────────────────────────────────────
Line 23 (start_line: 23, line: 23):
Severity: [concern]
Comment: The token is being logged to console - potential security issue

```typescript
// Current (problematic):
console.log("Token:", authToken);

// Suggested:
// Remove console.log or use a proper logger with redaction
```

─────────────────────────────────────

**Review Summary:**

- Total comments: 2
- Severity breakdown: 1 suggestion, 1 concern
- Estimated review time: 5 minutes

**Do you approve posting these comments as a review?** (yes/no/edit)

````

7. **Wait for user approval before posting anything.**

8. **Post the review using the proper review API (creates threaded comments):**

**IMPORTANT: Use the review API, NOT top-level PR comments.**

First, create the review object:

```bash
# Create a review (returns review ID)
gh api repos/{owner}/{repo}/pulls/<number>/reviews \
  -X POST \
  -f body='Reviewed the changes. See inline comments for specific feedback.' \
  -f event='COMMENT' \
  --jq '.id'
````

Then add individual review comments with proper line references:

```bash
# Comment on specific lines (use the review ID from above)
gh api repos/{owner}/{repo}/pulls/<number>/comments \
  -X POST \
  -f body='<comment text with code blocks>' \
  -f path='src/components/UserProfile.tsx' \
  -f line=52 \
  -f start_line=45 \
  -f side='RIGHT' \
  -f commit_id='<head_commit_sha>' \
  -f in_reply_to=<review_id>
```

**Required fields explained:**

- `path`: File path relative to repo root
- `line`: Ending line number of the comment range
- `start_line`: Starting line number (for multi-line comments)
- `side`: 'RIGHT' for PR changes, 'LEFT' for original
- `commit_id`: SHA of the commit being reviewed (get from `gh pr view`)

9. **Alternative: Use gh pr review for simpler reviews:**

If you just need to submit a review without specific line comments:

```bash
# Submit a review with general feedback
gh pr review <number> --comment -b "$(cat <<'EOF'
## Review Summary

### Changes reviewed:
- Component refactoring looks good
- Test coverage is adequate

### Suggestions:
1. Consider adding error boundaries
2. The loading state could be smoother

Overall: Nice work! A few minor suggestions above.
EOF
)"
```

10. **Approve or request changes (only if you mean it):**

```bash
# Approve
gh pr review <number> --approve -b "LGTM - approved with minor suggestions"

# Request changes
gh pr review <number> --request-changes -b "Needs changes - see inline comments"
```

## Anti-patterns

- **DO NOT post top-level PR comments** for code feedback - use review threads instead
- Posting many tiny comments that could be one coherent review
- Asking for changes without a reason and a suggested direction
- Approving while also leaving a blocking comment
- Not specifying exact line numbers (start_line and line)
- Forgetting to wait for user approval before posting

## Test plan

- Verify line numbers match the diff before posting
- Check that commit_id is the latest HEAD of the PR
- Confirm user approved the draft comments

## PR Review Comment Templates (copy-ready)

### Code Suggestion Template:

````text
**Issue:** <what's wrong or could be better>

**Suggested change:**
```<language>
<before>
````

**After:**

```<language>
<after>
```

**Why:** <explanation>

````

### Security Concern Template:

```text
**Security concern:** <vulnerability>

**Current code:**
```<language>
<vulnerable code>
````

**Suggested fix:**

```<language>
<secure code>
```

**Impact:** <what could go wrong>

````

### Performance Template:

```text
**Performance suggestion:** <issue>

**Current approach:**
```<language>
<code>
````

**Optimized alternative:**

```<language>
<better code>
```

**Expected improvement:** <metrics>

````

## Example Complete Review Workflow

```bash
# 1. Get PR info
gh pr view 123 --json number,headRefOid,files

# 2. View diff
gh pr diff 123

# 3. Draft comments (present to user for approval)
# ... user approves ...

# 4. Create review
gh api repos/owner/repo/pulls/123/reviews \
  -X POST \
  -f body='Reviewed - see inline comments' \
  -f event='COMMENT'

# 5. Add specific line comment
gh api repos/owner/repo/pulls/123/comments \
  -X POST \
  -f body='Consider using useMemo here to prevent unnecessary recalculations' \
  -f path='src/components/Chart.tsx' \
  -f line=34 \
  -f side='RIGHT' \
  -f commit_id='abc123'
````
