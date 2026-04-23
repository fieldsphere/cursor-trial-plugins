---
name: markdown-naming
description: Naming conventions for markdown files across the project, including Cursor configuration files and general documentation. Use when creating or renaming any .md or .mdc files.
---

# Markdown naming

These conventions keep filenames consistent and discoverable. Use **kebab-case** (lowercase with hyphens).

## Cursor Starter Pack layout

In this monorepo, **Cursor Starter Pack**’s root is **`plugins/cursor-starter-pack/`**; inside it, rules live under `rules/*.mdc`, agents under `agents/*.md`, skills under `skills/{name}/SKILL.md`. Application repositories use `.cursor/` at the project root with the same patterns; only the path prefix differs.

## Cursor configuration files

- **Rules** (project `.cursor/rules/*.mdc`, or plugin `rules/*.mdc`):
  - Pattern: `{domain}-{purpose}.mdc`
  - Examples: `design.mdc`, `api-security.mdc`, `git-workflow.mdc`, `code-quality.mdc`

- **Subagents** (project `.cursor/agents/*.md`, or plugin `agents/*.md`):
  - Pattern: `{role}-{specialization}.md`
  - Examples: `backend-eng.md`, `code-skeptic.md`, `ui-engineer.md`, `test-engineer.md`, `code-oracle.md`

- **Commands** (`.cursor/commands/*.md`):
  - Pattern: `{action}-{target}.md`
  - Examples: `create-ticket.md`, `generate-types.md`, `update-status.md`

- **Skills** (`skills/{name}/SKILL.md` in a plugin, or `~/.cursor/skills/{name}/` user skills):
  - Pattern: `{action}-{target}` (directory name)
  - Examples: `create-rule`, `learn`, `plan-change`

## General documentation

- **Documentation** (`*.md`): `{topic}-{type}.md` or `{topic}.md`
  - Examples: `api-reference.md`, `getting-started.md`

- **README**: always `README.md` (uppercase)

## Guidelines

- Always use kebab-case
- Be descriptive but concise (2–4 words typically)
- Avoid abbreviations unless widely understood
- Use consistent patterns within each category

## Creating markdown files

**Only create** new markdown when:

- The user asked for it
- Required for Cursor configuration (rules, subagents, commands)
- Essential project documentation (README, critical guides)

**Avoid** new files for temporary notes, content that belongs in code comments, or one-off explanations that could extend an existing doc.

When in doubt, ask the user. Prefer updating existing docs over adding files.

Use these conventions for new files; refactor existing ones when aligning names.
