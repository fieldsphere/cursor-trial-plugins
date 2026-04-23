---
name: browser-automation-tests
description: Verify product behavior with Cursor browser automation by driving real UI flows, capturing failures, and turning findings into actionable repro steps or follow-up tests. Use when the user asks for browser automation, in-browser verification, UI smoke checks, or manual flow testing in Cursor.
---

# Browser Automation Tests

Use Cursor browser automation to validate UI behavior in a running app, reproduce issues, and gather evidence for follow-up fixes or automated tests.

## Workflow

1. Confirm the target URL, environment, and success criteria for the flow.
2. Use browser automation to exercise the real UI path deliberately, one state change at a time.
3. Capture the important evidence: page state, visible failures, console issues, or network problems when relevant.
4. Summarize the observed behavior against the expected behavior.
5. If the user wants durable repo coverage afterward, hand off to `write-e2e-tests` or `test-engineer`.

## Principles

- Prefer short, purposeful flows over broad unscripted browsing.
- Validate the user-visible outcome after each action.
- Stop and report blockers such as login walls, missing data, or environment issues instead of guessing.
- Use browser automation for real runtime verification; use unit or E2E code tests for durable coverage in the repo.
- Keep notes concrete enough to become a bug report or automated test later.

## Output

- Flow exercised
- Expected behavior vs observed behavior
- Evidence collected
- Recommended next step: fix, add automated coverage, or investigate further
