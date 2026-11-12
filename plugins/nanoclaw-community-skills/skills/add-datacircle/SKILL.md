---
name: add-datacircle
description: Add Datacircle's open MCP server so the agent can compare GTM APIs and their plans by price, score and limits. No key needed.
---

# Add Datacircle

Find the best GTM APIs. Datacircle benchmarks all the GTM APIs and puts the results on its website, https://datacircle.dev. Its MCP server is open to anyone, with no key.

## Phase 1: Pre-flight

Check if `container/agent-runner/src/index.ts` already has `datacircle` in `mcpServers`. If so, skip to Phase 3.

## Phase 2: Apply Code Changes

In `container/agent-runner/src/index.ts`, add a second server next to `nanoclaw` in `mcpServers`:

```ts
datacircle: {
  type: 'http',
  url: 'https://api.datacircle.dev/mcp',
},
```

Add `'mcp__datacircle__*'` to the `allowedTools` list, then rebuild the container image.

## Phase 3: Verify

Ask the agent: "Which GTM API is cheapest for finding work emails?" It should call `list_apis` and `search_plans`.

The same data is a file at https://datacircle.dev/datacircle.json, and an open REST API at https://api.datacircle.dev/v1 (spec: https://api.datacircle.dev/v1/openapi.json). Skill file: https://datacircle.dev/SKILL.md.
