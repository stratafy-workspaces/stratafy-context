---
id: 836e9741-c7ad-4200-a3ef-86ddbfb547af
type: initiative
status: draft
priority: medium
strategy: Strategic AI Infrastructure
completionPercentage: 0
---

# MCP Server Optimisation

## Description
Optimise Stratafy's MCP server layer across two dimensions: (1) Permission-scoped tool exposure — tools surfaced to a client reflect what the API key actually permits, eliminating tool calls that will fail; (2) Semantic tool discovery via a search_tools meta-tool for context-window efficiency, reducing session token cost from 12-19K to ~3K. Dimension 3 (executive context bundling) moved to the Experts — Roster, Linking & Context Packaging initiative where it belongs architecturally.

## Parent Strategy
[Strategic AI Infrastructure](../strategy/product/strategic-ai-infrastructure.md)

## Status & Progress
- **Status**: draft
- **Priority**: medium
- **Completion**: 0%

## Key Objectives
No objectives defined

## Timeline
- **Start Date**: Not set
- **Target Date**: Not set

## Content
# MCP Server Optimisation

## Overview
Optimise Stratafy's MCP server layer across two dimensions. Both serve the general agent and expert paths equally.

## Scope Update (March 16, 2026)

Original scope had three dimensions. Dimension 3 (executive context bundling via `get_expert_context`) has been moved to the Experts — Roster, Linking & Context Packaging initiative (`f50412ff`). It depends on expert-to-strategy ownership mapping and context_profiles — both owned by that initiative.

This initiative now focuses on the two infrastructure concerns that serve all MCP consumers equally.

---

## Dimension 1: Permission-Scoped Tool Exposure

Tools surfaced to a client should reflect what the API key actually permits. The current behaviour exposes the full tool list regardless of role, meaning agents attempt calls they're not permitted to make, generating confusing errors and wasting context.

### What Exists
- `TOOL_PERMISSIONS` map: every tool → required permissions (284 lines, complete)
- `ToolScope` type: `'core' | 'agents' | 'workspace'` — crude group-level filtering via separate endpoints
- Permission resolution at request time (`resolveUserPermissions`)
- Per-tool permission checks on execution (tools fail with 403 if insufficient permissions)

### What's Missing
- Runtime tool-list filtering: at session init, inspect the resolved permissions and filter the tool manifest before sending to client
- A read-only API key should only see read tools in `tools/list`
- An agent token with `strategy:read` + `cortex:read` should see ~80 tools, not 233

### Implementation Approach
At `createMcpServerWithAuth()`, after permissions are resolved, filter `registerTrackedTool` calls to only register tools where the user's permissions satisfy `TOOL_PERMISSIONS[toolName]`. The `shouldRegister()` helper already exists for scope-based filtering — extend it with permission-based filtering.

---

## Dimension 2: Semantic Tool Discovery (`search_tools`)

A `search_tools` meta-tool that accepts a natural language query and returns the 3-5 most relevant tools with their schemas.

### The Problem
Current full tool manifest costs 12,000–19,000 tokens per session across 3 MCP servers. Most agent sessions use 3-8 tools. The rest is wasted context.

### The Solution
Rather than injecting all tool definitions at session start, provide a lightweight meta-tool:

```
search_tools(query: "update strategy completion percentage")

Returns:
[
  { name: "update_strategy", description: "...", inputSchema: {...} },
  { name: "update_initiative", description: "...", inputSchema: {...} },
  { name: "update_okr_score", description: "...", inputSchema: {...} },
]
```

### Token Impact
- Current: 12,000-19,000 tokens for full manifest
- With search_tools: ~2,000 tokens for the meta-tool + ~500 tokens per loaded tool
- Most sessions: 3-8 tools = 3,500-6,000 tokens (60-70% reduction)

### Implementation Options
- **Simple**: TF-IDF or keyword matching over tool names + descriptions (fast, no external dependency)
- **Semantic**: Embed tool descriptions with pgvector, cosine similarity search (better results, already have pgvector)
- **Hybrid**: Keyword match first, fall back to semantic if no good match

### Open Question
How does this interact with Dimension 1? If the tool list is already filtered by permissions, `search_tools` searches only within permitted tools. This is the correct behaviour — an agent shouldn't discover tools it can't use.

---

## Related Decisions
- Decision `3d804525` — Architectural boundary: Strategic AI Infrastructure owns MCP server optimisation

## Related Initiatives
- Hot Strategic Context Cache (`59dcf6b2`) — performance layer for both context tools
- Experts — Roster, Linking & Context Packaging (`f50412ff`) — now owns Dimension 3 (get_expert_context)
- Agent Registry & API Key Platform (`4c112c8e`) — general agent path that benefits from both dimensions

## Success Criteria
- 🔲 Permission-scoped tool manifest: agents only see tools they can use
- 🔲 `search_tools` meta-tool returning relevant tools from natural language queries
- 🔲 60%+ token reduction in average session tool manifest size
- 🔲 Zero increase in tool-call error rate (agents don't attempt forbidden calls)
