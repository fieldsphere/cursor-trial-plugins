# Cursor Starter Pack

Single Cursor plugin with foundational **code quality**, **software design**, everyday skills (**learn**, **commit**, **markdown-naming**, **agent-naming**), workflow skills (**plan-change**, **review-change**, **trace-defect**), **code-skeptic**, **ui-engineer**, **test-engineer**, and **code-oracle** agents, and optional **MCP** configuration.

This directory **is** the plugin root (`.cursor-plugin/`, `rules/`, `skills/`, `agents/`, `mcp.json`). Layout matches [Cursor plugins](https://cursor.com/docs/plugins).

In this repository, the plugin lives at **`plugins/cursor-starter-pack/`**. The manifest **`displayName`** is **Cursor Starter Pack**; the package **`name`** is **`cursor-starter-pack`**.

## Contents

| Path | Purpose |
|------|---------|
| `.cursor-plugin/plugin.json` | Manifest: `name` **cursor-starter-pack**, `displayName` **Cursor Starter Pack** |
| `rules/code-quality.mdc` | Security, structure, and quality for code in any language |
| `rules/system-design.mdc` | Boundaries, coupling, APIs, evolution, tradeoffs |
| `skills/learn/` | Ramp on an unfamiliar codebase |
| `skills/commit/` | Conventional Commits workflow |
| `skills/markdown-naming/` | Kebab-case naming for `.md`, `.mdc`, plugin layout |
| `skills/agent-naming/` | Consistent names for cloud and local agents (ticket vs non-ticket) |
| `skills/plan-change/` | Scope, acceptance criteria, risks, order of work |
| `skills/review-change/` | Structured PR/diff review checklist |
| `skills/trace-defect/` | Reproduce, narrow, hypotheses, evidence |
| `agents/` | `code-skeptic`, `ui-engineer`, `test-engineer`, `code-oracle` |
| `mcp.json` | Empty by default; customize per org |
| `mcp.template.json` | Example MCP entries to copy into `mcp.json` when needed |

## Skill and agent pairing

| Skill | Often pairs with |
|-------|------------------|
| `plan-change` | Manual planning; optional **test-engineer** then **code-skeptic** after implementation; optional **code-oracle** when the user asks for deep planning or architecture |
| `review-change` | **code-skeptic** for review and automated checks |
| `trace-defect` | Search and Cursor’s built-in **Explore** subagent to map unfamiliar code paths |

## Install (local)

1. Clone or open the **parent** repository (this file’s repo root).

   ```bash
   ln -sf /absolute/path/to/repo/plugins/cursor-starter-pack ~/.cursor/plugins/local/cursor-starter-pack
   ```

2. Restart Cursor or run **Developer: Reload Window**.

The symlink target must be **`plugins/cursor-starter-pack`**, not the monorepo root, so `.cursor-plugin/plugin.json` resolves correctly.

## Org-specific fork (optional)

1. Copy `plugins/cursor-starter-pack` to a new folder (e.g. `plugins/cursor-starter-pack-acme`) or fork the repo and add a sibling under `plugins/`.
2. Edit `.cursor-plugin/plugin.json` (`name`, `displayName`, `description`) so the bundle is unique.
3. Add rules under `rules/` (e.g. `generated-workspace-context.mdc`) with org goals, repos, and terminology.
4. Merge chosen servers from `mcp.template.json` into `mcp.json`; set env vars outside the chat.

If you add a new plugin directory, register it in the repo root [`.cursor-plugin/marketplace.json`](../../.cursor-plugin/marketplace.json).
