# Testing

Focused plugin for automated testing:

- **test-engineer** agent — Adds and extends unit and E2E tests to match repo conventions
- **test-runner** agent — Runs and interprets test commands when you need execution-only verification
- **`mcp.json`** — Empty by default; add CI or vendor MCP servers when needed

The **Cursor Starter Pack** still owns the universal expectation that behavior changes should be tested. This plugin owns the test-specific workflows: use `test-engineer` when coverage needs to be written or updated, `test-runner` when you want commands executed and failures summarized, and `code-skeptic` in Starter Pack when you want adversarial code review plus verification together.

Plugin id: **`testing`**. Display name: **Testing**.
