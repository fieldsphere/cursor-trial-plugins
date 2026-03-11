# Feature Flag Migration Plugin Pack

A Cursor plugin pack for migrating legacy feature flag systems to [OpenFeature](https://openfeature.dev/). Includes agents, rules, and skills that automate the full migration lifecycle: inventory, migration, verification, cleanup, and scaffolding new flags with OpenFeature from day one.

## What's Included

### Rules (`.cursor/rules/`)

| Rule | Scope | Purpose |
|------|-------|---------|
| `feature-flag-migration.mdc` | File-scoped | Migration principles, before/after patterns for Go and TypeScript |
| `no-new-legacy-flags.mdc` | Always-apply | Governance: blocks new legacy flag usage, enforces OpenFeature for new code |

### Agents (`.cursor/agents/`)

| Agent | Mode | Purpose |
|-------|------|---------|
| `feature-flag-inventory` | Read-only | Scans codebase for all flag usage, classifies migration status and staleness, produces a prioritized migration manifest |
| `feature-flag-migrator` | Read-write | Converts legacy flag evaluations to OpenFeature SDK calls, supports shadow/dual-evaluation for high-risk flags |
| `feature-flag-verifier` | Read-only | Independent reviewer that checks migration correctness, parity verification, and manifest compliance |
| `feature-flag-cleaner` | Read-write | Safely removes stale flags (deprecated, 100% rollout, unused) from both code and registry |
| `feature-flag-scaffolder` | Read-write | Scaffolds new flags with OpenFeature evaluation patterns, test setup, registry entry, and optional external provider creation via MCP |

### Skills (`.cursor/skills/`)

| Skill | Purpose |
|-------|---------|
| `openfeature-migration` | Step-by-step implementation guide for migrating Go and TypeScript flag evaluations, shadow mode patterns, phased rollout plan, testing setup |

## Migration Workflow

```
Phase 0: Setup          → Install this pack, configure OpenFeature provider
Phase 1: Discovery      → Run inventory agent → migration manifest
Phase 2: Migrate        → Run migrator agent per package (direct or shadow)
Phase 3: Validate       → Run verifier agent, monitor shadow parity logs
Phase 4: Decommission   → Run cleaner agent, remove legacy interface
Ongoing: New flags      → Run scaffolder agent (always uses OpenFeature)
```

## Installation

Copy the contents into your project's `.cursor/` directory:

```bash
cp -r rules/ /path/to/project/.cursor/rules/
cp -r agents/ /path/to/project/.cursor/agents/
cp -r skills/ /path/to/project/.cursor/skills/
```

Then customize the file-glob patterns in `feature-flag-migration.mdc` and the legacy patterns in agent files to match your codebase's flag system.

## Adapting to Your Codebase

This pack was built against Grafana's feature flag system. To adapt:

1. **Legacy patterns**: Update the Grep patterns in the inventory and migrator agents to match your SDK (e.g., `ldClient.variation()`, `useFlags()`, `LaunchDarkly.get()`)
2. **OpenFeature patterns**: The OpenFeature SDK calls are standard and shouldn't need changes
3. **Registry**: Replace references to `registry.go` with your flag definition source
4. **MCP**: The inventory and scaffolder agents optionally use LaunchDarkly via MCP; configure for your provider
5. **Governance rule**: Update `no-new-legacy-flags.mdc` with your legacy SDK's import/call patterns
6. **Scaffolder**: Update the test setup examples and import paths to match your project's testing conventions
