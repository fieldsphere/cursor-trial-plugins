---
name: git-hygiene
description: Keep git history clean and reviewable with branch naming, branch upkeep, merge conflict handling, and pull request prep. Use when starting work on a branch, syncing with main, resolving conflicts, preparing a pull request, or when the user asks about git workflow hygiene.
---

# Git hygiene

## Goal

Create small, safe, reviewable changes without rewriting or obscuring other engineer's work.

## When to apply

- Starting a new change
- Cleaning up a branch before push
- Syncing with `main`
- Resolving merge conflicts
- Preparing or updating a pull request

## Workflow

1. **Start clean**
   - Check `git status` before making changes.
   - If the worktree is dirty, separate unrelated changes before continuing.

2. **Name branches clearly**
   - Use kebab-case.
   - Prefer `{type}/{scope}-{description}`.
   - Examples: `feature/auth-session-timeout`, `fix/api-null-check`, `docs/readme-local-setup`

3. **Keep branches short-lived**
   - Prefer focused branches and small diffs.
   - Sync with `main` regularly to reduce conflict size.
   - Avoid stacking unrelated work on one branch.

4. **Keep commits atomic**
   - One logical change per commit.
   - Do not mix refactors, formatting, and feature work unless they are inseparable.
   - Use the `commit` skill for commit message formatting.

5. **Resolve conflicts deliberately**
   - Read both sides before editing.
   - Preserve behavior intentionally; do not accept one side blindly.
   - After resolving, rerun relevant tests or checks.

6. **Prepare a reviewable pull request**
   - Review the final diff before opening the PR.
   - Summarize what changed, why, and how it was tested.
   - Call out risky areas, follow-ups, and known gaps.

## Pull request checklist

- Branch name is specific and scoped
- Diff only contains intended changes
- No leftover debug code, temporary logs, or commented-out blocks
- Relevant tests or checks were run
- PR description includes summary and test plan

## Safety rules

- Never run destructive git commands unless the user explicitly asks
- Do not rewrite shared history without clear approval
- Avoid force-push on shared branches
- Do not "fix" conflicts by dropping code you do not understand
- If unexpected repo changes appear, pause and ask how to proceed

## What to avoid

- Vague branch names like `update`, `stuff`, or `misc-fixes`
- Large mixed-purpose branches
- Blind conflict resolution
- Opening a PR without reviewing the diff
- Combining unrelated cleanup with functional changes
