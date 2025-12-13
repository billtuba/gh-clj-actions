# gh-clj-actions Development Guidelines

## Project Overview

This repository provides reusable GitHub Actions for Clojure projects. It's designed to be simple, focused, and automatically maintained through Renovate and automated tagging.

## Git Workflow - Protecting Main

**Every change must follow this workflow to keep main clean:**

1. **Create a new branch** at the start of any feature work
   ```bash
   git checkout -b feature-name
   ```

2. **Make changes** to action files, workflows, or documentation

3. **Ask human to provide commit message** - AI must ASK the human "What commit message would you like?" and wait for the human's response. Never draft or suggest commit messages.

4. **Commit with conventional format**:
   ```bash
   git add .
   git commit -m "commit message

   🤖 Generated with [Claude Code](https://claude.com/claude-code)

   Co-Authored-By: Claude Sonnet 4.5 <noreply@anthropic.com>"
   ```

5. **Push branch and open PR**:
   ```bash
   git push -u origin feature-name
   gh pr create --title "..." --body ""
   ```

6. **Watch the build**:
   ```bash
   gh pr checks <pr-number> --watch
   ```
   - The test workflow will verify the action still works correctly
   - All tests must pass before merging

7. **If build passes, merge and cleanup**:
   ```bash
   gh pr merge <pr-number> --squash --delete-branch
   git checkout main
   git pull
   ```

8. **Auto-tagging happens automatically**:
   - When PR merges to main, the `auto-tag.yml` workflow runs
   - It automatically updates the `v1` tag to point to the latest commit
   - No manual tag management needed!

**Key principles:**
- ✅ **Never commit directly to main**
- ✅ **Always let CI run tests before merging**
- ✅ **Each feature gets its own branch and PR**
- ✅ **Clean history: one feature = one PR**
- ❌ **Never let multiple features accumulate uncommitted on main**

## Testing

- The `.github/workflows/test.yml` workflow runs automatically on every PR
- It verifies that the `setup-env` action works correctly
- Tests must pass before merging

## Renovate Updates

- Renovate runs weekly (Saturday 6am America/Chicago)
- Creates PRs for GitHub Actions updates and Clojure dependency updates
- Review the PR, ensure tests pass, then merge
- The v1 tag updates automatically after merge

## Remember

This is a simple Actions repository. Keep changes focused and ensure the test workflow passes before merging.
