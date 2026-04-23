# Cursor Fundamentals

**Cursor Fundamentals** (`cursor-fundamentals`) is a Cursor Team Marketplace built around one idea: give every function a small, focused plugin that encodes how the team actually works. Each plugin contributes the minimum set of rules, skills, agents, and MCP servers needed to raise quality in that function without overlapping with the others.

## Plugins

### Cursor Starter Pack

Engineering baseline that every contributor gets by default. It ships the non-negotiables: code quality and system design rules, a repo-onboarding skill, commit and git hygiene, planning output, and the naming conventions that make markdown files and Cursor agents consistent across the org. The `code-skeptic` and `code-oracle` agents handle critical review and deeper architectural reasoning when a change needs a second set of eyes. Start here; most other plugins assume this one is installed.

### Product Management

Owns everything between "we should build this" and "engineering can execute on it." Use it to draft implementation-ready Jira tickets, summarize a board or sprint for a stakeholder update, and stress-test a plan with the `devils-advocate` agent before any code is written. The included Atlassian MCP wires the plugin into Jira and Confluence so ticket reading and writing stay in the loop.

### Design

Covers UX definition and the handoff into code. The `wireframes` and `mockup` skills help teams reason about backend-aware UI states and high-fidelity layouts, the `component-designer` agent focuses on component-level decisions, and the `ui-engineer` agent implements the result in a way that respects the design intent. The Figma MCP keeps Figma files and code aligned without context switching.

### Technical Writing

The single home for developer-facing prose. It generates and updates READMEs, produces weekly review summaries, and flags when a code change should trigger a README update (`readme-hygiene`). The `docs-writer` agent handles longer-form documentation such as API references and guides. An optional Notion MCP is included for teams that publish there. Markdown file-naming conventions intentionally live in **Cursor Starter Pack** so naming stays universal rather than docs-specific.

### Testing

Focused specifically on automated tests. The `test-engineer` agent adds and extends unit and E2E tests that match the project's frameworks and conventions, and the `test-runner` agent runs and interprets the relevant test commands. `mcp.json` is intentionally empty so each team can add CI or vendor MCP servers that fit their stack.

## Repository structure

- `.cursor-plugin/marketplace.json`: marketplace manifest and plugin registry
- `plugins/<plugin-name>/.cursor-plugin/plugin.json`: per-plugin metadata
- `plugins/<plugin-name>/rules`: rule files (`.mdc`)
- `plugins/<plugin-name>/skills`: skill folders with `SKILL.md`
- `plugins/<plugin-name>/agents`: subagent definitions
- `plugins/<plugin-name>/mcp.json`: MCP server configuration for each plugin

## Use this marketplace on your team

Cursor Fundamentals is a template. Teams fork the repo, tailor the plugins to their own conventions, and register the fork as a **Team Marketplace** from the Cursor dashboard.

### 1. Fork the repo

1. Fork this repository to your team's GitHub organization (for example, `your-org/cursor-fundamentals`).
2. Clone the fork locally and edit plugin contents (`rules/`, `skills/`, `agents/`, `mcp.json`) to reflect your stack, conventions, and tooling. Remove plugins you don't want.
3. If you rename the marketplace, update both `name` (lowercase kebab-case) and `displayName` in [.cursor-plugin/marketplace.json](.cursor-plugin/marketplace.json).
4. Run `node scripts/validate-template.mjs` to catch manifest, frontmatter, and path issues before publishing.
5. Commit and push. If the repo is private, grant the Cursor GitHub app read access when prompted in the next step.

### 2. Register the fork in the Cursor dashboard

In Cursor, go to **Dashboard → Settings → Plugins**, click **Import**, paste your fork's GitHub URL, then:

- Choose the **access group(s)** that should see these plugins.
- For each plugin, mark it **Required** (auto-installed for that group) or **Optional** (developer choice).
- Save. Cursor syncs new commits on the default branch, so pushing to the fork is how you ship updates.

Notes:

- **Teams** plan: up to 1 team marketplace. **Enterprise** plan: unlimited team marketplaces.
- Members of the selected access groups will see the plugins in **Settings → Plugins** inside Cursor.

## Further reading

- [Cursor Plugins documentation](https://cursor.com/docs/plugins) — plugin anatomy (rules, skills, agents, commands, MCP, hooks) and team-marketplace setup.
- [Cursor Marketplace](https://www.cursor.com/marketplace) — officially reviewed plugins you can use as references.
- [cursor/plugin-template](https://github.com/cursor/plugin-template) — minimal starter for building a single plugin or multi-plugin marketplace.
- [Team dashboard](https://cursor.com/docs/account/teams/dashboard) — where team marketplaces are imported and managed.
