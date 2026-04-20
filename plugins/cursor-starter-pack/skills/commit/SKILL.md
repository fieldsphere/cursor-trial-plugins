---
name: commit
description: Create commits with conventional commit messages. Analyzes staged changes, generates a short one-line message, and runs git commit. Use when the user asks to commit, write a commit message, or create a commit.
---

# Commit messages

## When to apply

- User asks to commit (staged or unstaged changes)
- User wants a commit message or to create a commit
- User asks to review or summarize what will be committed (then offer to commit)

## Format: Conventional Commits (one line)

```
<type>(<scope>): <subject>
```

**Type** (required): `feat`, `fix`, `docs`, `style`, `refactor`, `test`, `chore`

**Scope** (optional): affected area (e.g. `auth`, `tournament`, `ui`)

**Subject** (required): imperative mood, lowercase after type, no period. Keep under ~40 chars.

## Examples (short)

```
feat(tournament): add date formatting
fix(reports): correct timezone in dates
refactor(api): extract date util
chore: add commit-messages skill
docs: update README setup
```

## Workflow

1. Run `git status` and `git diff --staged` to see staged changes
2. If nothing is staged but there are modified files, run `git add` for the modified files (or all with `git add -u`) before committing
3. Infer type and scope from the changes
4. Write a single-line subject in imperative mood
5. Run `git commit -m "<message>"` to create the commit

## Rules

- One line only; no body or footer unless user explicitly requests
- Subject under ~40 characters; omit scope if message stays clear without it
- No period at end of subject
- Actually run `git commit`; do not just suggest the message
