---
name: write-unit-tests
description: Write focused unit tests that match the repository's existing test stack and conventions. Use when the user asks for unit tests, logic coverage, regression coverage for functions or modules, or fast isolated test cases.
---

# Write Unit Tests

Add or update unit tests that exercise logic, branching, edge cases, and failure modes without pulling in unnecessary end-to-end coverage.

## Workflow

1. Discover the existing unit-test framework, helpers, and file layout.
2. Identify the exact functions, modules, or boundaries that changed.
3. Cover the most important success paths, edge cases, and error behavior.
4. Mock external I/O only at the boundaries already used by the repo.
5. Run the narrowest relevant test command when possible.

## Principles

- Prefer fast, isolated tests over broad integration behavior.
- Match the repository's current patterns; do not introduce a new test framework without approval.
- Cover behavior, not implementation details.
- Keep fixtures and mocks minimal and readable.
- Add one test for each meaningful branch or failure mode, not duplicate coverage.

## Output

- Files added or updated
- Behaviors covered
- Commands run and results, or a blocker if tests could not run
