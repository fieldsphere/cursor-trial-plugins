---
name: plan-output
description: Shape implementation plans into a concise, execution-ready format with problem, scope, acceptance criteria, risks, steps, and verification. Use in Plan mode or when the user asks for a plan.
---

# Plan output

## Goal

Turn planning work into an actionable artifact which is easy to review and execute.

## Use this in plans for

- Features
- Refactors
- Migrations
- Debugging

## Default shape

Use this structure unless the user asks for something else:

1. **Overview**
   - One short paragraph describing changes and providing reasoning.

2. **Scope**
   - In scope: affected areas, files, systems, or behaviors.
   - Out of scope: anything intentionally excluded.

3. **Acceptance criteria**
   - 2-5 testable bullets defining "done".

4. **Risks**
   - Key failure modes, trade-offs, dependencies, or rollout concerns.

5. **Implementation steps**
   - Ordered steps from first change to last.
   - Prefer smallest shippable increments.

6. **Verification**
   - Tests, checks, or manual validation steps.

## Output rules

- Keep plans concise by default
- Prefer concrete nouns over vague phrases
- Make each step observable and actionable
- Call out assumptions when requirements are unclear, ask follow up questions to gain clarity
- Include "out of scope" when it prevents plan creep
- Do not pad with obvious filler

## Example skeleton

```md
## Problem
<what is changing and why>

## Scope
- In scope: ...
- Out of scope: ...

## Acceptance Criteria
- ...
- ...

## Risks
- ...

## Implementation Steps
1. ...
2. ...

## Verification
- ...
```
