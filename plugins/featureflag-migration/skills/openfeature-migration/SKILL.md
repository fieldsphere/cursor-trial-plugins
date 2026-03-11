---
name: openfeature-migration
description: Migrate Grafana feature flag evaluations from the legacy FeatureToggles interface to the OpenFeature SDK. Use when migrating IsEnabled/IsEnabledGlobally calls to OpenFeature, converting frontend config.featureToggles checks to React hooks, or implementing new flag evaluations.
---

# OpenFeature Migration

This skill covers the exact mechanics of converting legacy feature flag evaluations to the OpenFeature SDK in the Grafana codebase.

## Prerequisites

Read the rule file at `.cursor/rules/feature-flag-migration.mdc` for principles. This skill covers implementation specifics.

## Go Backend Migration

### Step 1: Identify the Legacy Call

Legacy patterns to find:

```go
// Pattern A: context-aware check
s.features.IsEnabled(ctx, featuremgmt.FlagXxx)

// Pattern B: global check (no context)
s.features.IsEnabledGlobally(featuremgmt.FlagXxx)

// Pattern C: helper function
featuremgmt.AnyEnabled(s.features, featuremgmt.FlagA, featuremgmt.FlagB)

// Pattern D: boot data / frontend settings
hs.Features.GetEnabled(ctx)
```

These are typically accompanied by `//nolint:staticcheck` comments.

### Step 2: Replace with OpenFeature Client

**For `IsEnabled(ctx, flag)` → `BooleanValue`:**

```go
import "github.com/open-feature/go-sdk/openfeature"

client := openfeature.NewDefaultClient()
enabled, _ := client.BooleanValue(
    ctx,
    featuremgmt.FlagXxx,
    false, // default must match legacy behavior
    openfeature.TransactionContext(ctx),
)
if enabled {
    // gated behavior
}
```

**For `IsEnabledGlobally(flag)` → `BooleanValue` with background context:**

```go
client := openfeature.NewDefaultClient()
enabled, _ := client.BooleanValue(
    context.Background(),
    featuremgmt.FlagXxx,
    false,
    openfeature.EvaluationContext{},
)
```

**For `AnyEnabled(features, flagA, flagB)` → multiple evaluations:**

```go
client := openfeature.NewDefaultClient()
aEnabled, _ := client.BooleanValue(ctx, featuremgmt.FlagA, false, openfeature.TransactionContext(ctx))
bEnabled, _ := client.BooleanValue(ctx, featuremgmt.FlagB, false, openfeature.TransactionContext(ctx))
if aEnabled || bEnabled {
    // gated behavior
}
```

**For `GetEnabled(ctx)` — leave as-is.** This method is used for boot data and cache keys. It does not have a direct OpenFeature equivalent and should remain until the boot data pipeline is refactored.

### Step 3: Remove the Legacy Dependency

If the `FeatureToggles` interface was injected solely for the migrated call(s):

1. Remove the field from the struct
2. Remove the constructor parameter
3. Update Wire bindings if needed (`make gen-go`)

If other legacy calls remain in the same struct, keep the injection.

### Step 4: Clean Up

- Remove `//nolint:staticcheck` comment from the migrated line
- Remove unused `featuremgmt` imports if the struct no longer uses `FeatureToggles`
- Run `go vet ./path/to/package/` to verify

## TypeScript Frontend Migration

### Step 1: Identify the Legacy Call

```typescript
// Pattern A: config object check
import { config } from '@grafana/runtime';
if (config.featureToggles.myFeature) { ... }

// Pattern B: boot data direct access
const featureToggles = config.featureToggles;
const isEnabled = featureToggles?.myFeature;
```

### Step 2: Replace — React Components

For code inside React components, use the hook:

```typescript
import { useBooleanFlagValue } from '@openfeature/react-sdk';

function MyComponent() {
  const myFeatureEnabled = useBooleanFlagValue('myFeature', false);

  if (!myFeatureEnabled) {
    return null;
  }
  // ...
}
```

### Step 3: Replace — Non-React Code

For utilities, services, or code outside React component trees:

```typescript
import { getFeatureFlagClient } from '@grafana/runtime/internal';

function doSomething() {
  if (getFeatureFlagClient().getBooleanValue('myFeature', false)) {
    // gated behavior
  }
}
```

Rules:
- Never cache `getFeatureFlagClient()` or its return values
- Call just-in-time at the point of evaluation
- Prefer hooks in React code; use the client only when hooks are unavailable

### Step 4: Clean Up

- Remove `import { config } from '@grafana/runtime'` if no longer needed
- Remove references to `config.featureToggles` if fully migrated
- Run `yarn typecheck` to verify

## Non-Boolean Flags

OpenFeature supports multiple value types. Grafana's `Expression` field can hold strings, numbers, and JSON:

```go
// String flag
val, _ := client.StringValue(ctx, "myStringFlag", "default", openfeature.TransactionContext(ctx))

// Integer flag
val, _ := client.IntValue(ctx, "myIntFlag", 0, openfeature.TransactionContext(ctx))

// Float flag
val, _ := client.FloatValue(ctx, "myFloatFlag", 0.0, openfeature.TransactionContext(ctx))

// Object/JSON flag
val, _ := client.ObjectValue(ctx, "myObjectFlag", map[string]any{}, openfeature.TransactionContext(ctx))
```

## Testing Migrated Code

### Go Tests

Use the in-memory provider in tests:

```go
import (
    "github.com/open-feature/go-sdk/openfeature"
    "github.com/open-feature/go-sdk/openfeature/memprovider"
)

func TestMyFeature(t *testing.T) {
    mp := memprovider.NewInMemoryProvider(map[string]memprovider.InMemoryFlag{
        featuremgmt.FlagXxx: {
            State:          memprovider.Enabled,
            DefaultVariant: "on",
            Variants: map[string]any{
                "on":  true,
                "off": false,
            },
        },
    })
    openfeature.SetProviderAndWait(mp)
    defer openfeature.SetProviderAndWait(openfeature.NoopProvider{})

    // test code that evaluates the flag
}
```

### Frontend Tests

Use `@grafana/test-utils` or mock the OpenFeature provider:

```typescript
import { OpenFeature, InMemoryProvider } from '@openfeature/web-sdk';

beforeEach(async () => {
  const provider = new InMemoryProvider({
    myFeature: { variants: { on: true, off: false }, defaultVariant: 'on', disabled: false },
  });
  await OpenFeature.setProviderAndWait('test', provider);
});
```

## Shadow / Dual-Evaluation Mode

For high-risk flags or large-scale migrations, use shadow evaluation to verify parity between the legacy and OpenFeature systems before fully switching over.

### Concept

Shadow mode evaluates a flag through **both** the legacy `FeatureToggles` interface and the OpenFeature client, compares the results, and logs any mismatches. The legacy result is used for actual behavior; the OpenFeature result is logged only.

### Evaluation Modes

| Mode | Legacy | OpenFeature | Used for behavior | Logs comparison |
|------|--------|-------------|-------------------|-----------------|
| `legacy-only` | Yes | No | Legacy | No |
| `shadow` | Yes | Yes | Legacy | Yes |
| `openfeature-primary` | Yes | Yes | OpenFeature | Yes |
| `openfeature-only` | No | Yes | OpenFeature | No |

### Go Implementation Pattern

```go
func evaluateWithShadow(ctx context.Context, features featuremgmt.FeatureToggles, flagName string, logger log.Logger) bool {
    legacyResult := features.IsEnabled(ctx, flagName) //nolint:staticcheck

    client := openfeature.NewDefaultClient()
    ofResult, _ := client.BooleanValue(ctx, flagName, false, openfeature.TransactionContext(ctx))

    if legacyResult != ofResult {
        logger.Warn("Feature flag parity mismatch",
            "flag", flagName,
            "legacy", legacyResult,
            "openfeature", ofResult,
        )
    }

    // In shadow mode, return legacy result. In openfeature-primary mode, return ofResult.
    return legacyResult
}
```

### TypeScript Implementation Pattern

```typescript
function evaluateWithShadow(flagName: string, legacyValue: boolean): boolean {
  const ofValue = getFeatureFlagClient().getBooleanValue(flagName, false);

  if (legacyValue !== ofValue) {
    console.warn(`Feature flag parity mismatch: ${flagName}`, {
      legacy: legacyValue,
      openfeature: ofValue,
    });
  }

  return legacyValue;
}
```

### When to Use Shadow Mode

- Flags that gate critical paths (auth, data access, billing)
- Flags with complex targeting rules or per-tenant evaluation
- During the first batch of migrations to build confidence
- When the flag's `Expression` is non-trivial (not just "true"/"false")

### When to Skip Shadow Mode

- Simple boolean flags with `Expression: "false"` (the common case)
- Flags used only in tests or dev mode
- Flags already at GA stage with `Expression: "true"` (always on)

## Phased Migration Plan

Migrate progressively, validating at each phase before advancing:

### Phase 0: Setup
- Rules, skill, and agents are in place (this file)
- OpenFeature provider is initialized (already done in `openfeature.go`)
- No code changes to evaluation sites yet

### Phase 1: Discovery and Cleanup
- Run the `feature-flag-inventory` agent to produce a migration manifest
- Identify and remove stale flags (100% rollout, deprecated, no code references)
- Output: prioritized migration manifest grouped by package/service

### Phase 2: Migrate by Package
- For each package/service group, run the `feature-flag-migrator` agent
- Low-risk flags (simple boolean, Expression: "false"): migrate directly
- High-risk flags: use shadow mode first, validate, then fully switch
- Each batch produces a reviewable PR

### Phase 3: Shadow Validation (high-risk flags only)
- Deploy shadow-mode code to a staging environment
- Monitor parity logs for mismatches
- Iterate until parity is confirmed
- Switch to `openfeature-primary` mode, then `openfeature-only`

### Phase 4: Finalize and Decommission
- Run `feature-flag-verifier` against the full codebase
- Remove any remaining shadow evaluation wrappers
- Remove `FeatureToggles` interface injection from fully-migrated services
- The `no-new-legacy-flags` rule prevents regression

## Verification Checklist

After migrating each call site:

- [ ] Flag name matches the `featuremgmt` constant exactly
- [ ] Default value matches legacy behavior (usually `false`)
- [ ] `TransactionContext(ctx)` is passed when a request context is available
- [ ] `//nolint:staticcheck` comment removed
- [ ] Unused `FeatureToggles` injection removed if applicable
- [ ] Tests pass: `go test ./path/...` or `yarn test path/to/file`
- [ ] Lint passes: `go vet ./path/...` or `yarn lint`
- [ ] Shadow mode used for high-risk flags (if applicable)
- [ ] No parity mismatches in shadow logs (if applicable)
