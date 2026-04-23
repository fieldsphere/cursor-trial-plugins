---
name: agent-naming
description: >-
  Names Cursor cloud and local agents consistently. When starting an agent from a
  ticket or issue, uses TICKET-ID plus a short Title Case description after a
  colon. When there is no ticket, uses Title Case with at most four words. Use
  whenever naming a new agent, cloud agent, background agent, or when the user
  mentions agent titles or agent naming. Applies to any agent that appears in
  the Agents sidebar.
---

# Agent naming conventions

Apply these rules when choosing the **name** or **title** for a Cursor agent (including cloud agents).

## Scope

These rules apply to **any agent session that appears in the Agents sidebar** (cloud, local, background, etc.). The same patterns apply whether the name is set in a dedicated field or shown as the row title in that list.

## When to apply the pattern

- **At creation** — When starting a new agent, set the title using the ticket-backed or non-ticket pattern before or as the session is created.
- **When renaming** — If an agent already appears in the sidebar with a generic or auto-filled title, rename it to match these rules.
- **After duplicate** — If duplicating an agent copies a vague title, rename the new session to a clear, pattern-compliant name.

## Product defaults

Cursor may pre-fill a title from the first line of the prompt or a generic label. Those defaults **do not** follow this skill until you **rename** the agent. Treat renaming as the step that aligns the sidebar with these conventions.

## Why it matters

Consistent names make **parallel runs and history** easy to scan in the sidebar without opening each thread.

## Ticket-backed agents

If the agent run is tied to a work item (ticket, issue, Linear/Jira/GitHub issue, etc.):

**Pattern:** `{TICKET-ID}: {Description}`

| Part | Rule |
|------|------|
| `TICKET-ID` | The identifier exactly as in the tracker (e.g. `CUR-123`, `FE-42`, `#891`). No extra spaces. |
| `Description` | Short phrase in **Title Case** (capitalize each word). Omit articles when possible. |

**Examples:**

- `CUR-891: Fix Terminal Scroll Jump`
- `FE-42: Add Weather Popover`
- `DEMO-7: Backend API Tests`

## Non-ticket agents

If there is **no** ticket or issue:

**Pattern:** `{Word1} {Word2} {Word3} {Word4}` (Title Case, **at most four words**)

| Rule | Detail |
|------|--------|
| Capitalization | Each word starts with a capital letter (Title Case). |
| Length | **Maximum four words** total. |
| Content | Prefer a clear action or scope (what the agent is doing). |

**Examples:**

- `Refactor IDE Tab Bar`
- `Investigate Flaky Test`
- `Document API Endpoints`

## Quick decision

1. Is there a ticket/issue ID? → Use **Ticket-backed** pattern.
2. Otherwise → Use **Non-ticket** pattern (≤4 words, Title Case).
