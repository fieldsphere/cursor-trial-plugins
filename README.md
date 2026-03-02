# Cursor Trial Plugins

Build and publish Cursor Marketplace plugins from a single repository.

## Included plugins

This repo currently ships five grouped plugins:

- **git-workflows**: commit, PR, CI, merge conflict, and branch validation workflows
- **documentation**: README updates, weekly review summaries, markdown naming, and docs writing
- **pm**: Jira-oriented PM workflows with MCP config, ticket writing, and board summarization
- **design**: wireframes, component design support, and mockup workflow
- **testing-reliability**: Datadog dashboards, performance optimization, and testing agents

Starter references are still available under `plugins/starter-simple` and `plugins/starter-advanced`.

## Repository structure

- `.cursor-plugin/marketplace.json`: marketplace manifest and plugin registry
- `plugins/<plugin-name>/.cursor-plugin/plugin.json`: per-plugin metadata
- `plugins/<plugin-name>/rules`: rule files (`.mdc`)
- `plugins/<plugin-name>/skills`: skill folders with `SKILL.md`
- `plugins/<plugin-name>/agents`: subagent definitions
- `plugins/<plugin-name>/mcp.json`: MCP server configuration for each plugin

## Validate changes

Run:

```bash
node scripts/validate-template.mjs
```

This checks marketplace paths, plugin manifests, and required frontmatter in rule/skill/agent/command files.

## Submission checklist

- Each plugin has a valid `.cursor-plugin/plugin.json`
- Plugin names are unique, lowercase, and kebab-case
- `.cursor-plugin/marketplace.json` entries map to real plugin folders
- Required frontmatter metadata exists in plugin content files
- Logo paths resolve correctly from each plugin manifest
- `node scripts/validate-template.mjs` passes
