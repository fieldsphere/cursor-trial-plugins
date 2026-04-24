# Testing

Focused plugin for automated testing:

- **write-unit-tests** skill — Focused unit-test authoring for logic, branches, and edge cases
- **write-e2e-tests** skill — End-to-end coverage for real user journeys
- **browser-automation-tests** skill — Cursor browser automation for runtime UI verification and repro steps
- **test-engineer** agent — Adds and extends unit and E2E tests to match repo conventions
- **test-runner** agent — Runs and interprets test commands when you need execution-only verification
- **`mcp.json`** — Empty by default; add CI or vendor MCP servers when needed

The **Cursor Starter Pack** still owns the universal expectation that behavior changes should be tested. This plugin owns the test-specific workflows: use `write-unit-tests` for narrow logic coverage, `write-e2e-tests` for durable user-journey coverage, `browser-automation-tests` for live UI verification in Cursor, `test-engineer` when coverage needs to be written or updated across test types, `test-runner` when you want commands executed and failures summarized, and `code-skeptic` in Starter Pack when you want adversarial code review plus verification together.

Plugin id: **`testing`**. Display name: **Testing**.
