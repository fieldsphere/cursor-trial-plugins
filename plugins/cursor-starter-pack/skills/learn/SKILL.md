---
name: learn
description: Learn an unfamiliar codebase—structure, entry points, how to run and test, and where to change things safely. Use when joining a project, switching teams, or ramping on a new repo.
---

# Learn the project

## Goal
Build a practical mental model: what the system does, how it is organized, and how you can work on it without breaking things.

## Steps

1. **Basic Knowledge**
   - Read the README, understand the purpose of the project, and find relevant documentation.
   - Note runtime, package manager, and how to run the app and tests locally.

2. **Codebase**
   - Understand the architecture of the application. Find main entry points (apps, services, CLIs).
   - Identify major domains (auth, data, UI, jobs) and how they connect.
   - Trace a vertical slice (e.g. one user flow or API) with search, or use Cursor’s built-in **Explore** subagent when you want isolated exploration.

3. **Tooling**
   - List MCP servers that help (docs, tickets, design); configure env vars outside chat.
   - List relevant extensions or services needed for this project.

4. **Recent Activity**
   - Identify top contributors in the relevant part of the codebase or repo.
   - Note the most recent additions or significant changes to understand current direction and active areas.
   - Use recent commits, blame, or PR history as signals, not ground truth for ownership.

5. **Warnings**
   - Call out non-standard patterns, local conventions, or fragile areas of the codebase.
   - Note places where adding new code is risky: hidden coupling, generated files, migrations, legacy flows, custom tooling, or unusual deployment assumptions.
   - Warn about additions that may require extra validation, coordination, or documentation updates.



## Output
A short summary: what the project does, how it is laid out, how to run and test it, top contributors, recent additions, non-standard warnings, open questions, and what to read or explore next.
