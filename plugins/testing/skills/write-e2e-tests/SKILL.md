---
name: write-e2e-tests
description: Write end-to-end tests for real user journeys using the repository's existing browser or application test stack. Use when the user asks for E2E tests, workflow coverage, UI regression protection, or multi-step journey validation.
---

# Write E2E Tests

Add or update end-to-end tests that protect critical user flows from the user's point of view.

## Workflow

1. Discover the existing E2E framework, fixtures, selectors, helpers, and file layout.
2. Pick the smallest set of user journeys that materially reduces regression risk.
3. Reuse stable selectors, page objects, and fixtures that already exist in the repo.
4. Cover the happy path and one meaningful failure, guard, or empty-state path when relevant.
5. Run the targeted E2E command when possible and summarize failures clearly.

## Principles

- Test real user behavior, not internal implementation details.
- Prefer stable selectors and existing abstractions over brittle DOM coupling.
- Keep flows realistic and deterministic.
- Avoid overlapping the same behavior across too many E2E cases.
- If the repo has no E2E stack, ask before introducing one.

## Output

- Files added or updated
- User journeys covered
- Commands run and results, or a blocker if the environment could not run the flow
