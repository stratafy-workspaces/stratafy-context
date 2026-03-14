---
id: 59dcf6b2-ac4b-428b-943b-cbf5779220a7
type: initiative
status: active
priority: medium
strategy: Strategic AI Infrastructure
completionPercentage: 0
---

# Hot Strategic Context Cache

## Description
Build a pre-computation and caching layer for frequently accessed strategic context. Materialized views for workspace snapshots, strategy trees, current priorities, and active risks. Target: <100ms for an AI agent to have full strategic context when a conversation begins (vs current 2-3 seconds of sequential MCP calls). Critical for the "strategy available wherever decisions happen" vision — if strategic context is slow to load, people won't use it in the flow of work. Evaluate: Redis/Upstash for hot cache, PostgreSQL materialized views for warm cache, invalidation via Supabase Realtime.

## Parent Strategy
[Strategic AI Infrastructure](../strategy/product/strategic-ai-infrastructure.md)

## Status & Progress
- **Status**: active
- **Priority**: medium
- **Completion**: 0%

## Key Objectives
- [40% reduction in token usage per AI interaction](../objectives/40-reduction-in-token-usage-per-ai-interaction.md)
- [Context assembly time under 200ms with ≥ 80% cache hit rate](../objectives/context-assembly-time-under-200ms-with-80-cache-hit-rate.md)

## Timeline
- **Start Date**: Not set
- **Target Date**: 2026-06-30

## Content
# Hot Strategic Context Cache

## The Problem

Every AI interaction with Stratafy requires assembling strategic context: fetching the relevant strategies, initiatives, risks, assumptions, and metrics to give the AI agent enough context to respond intelligently. Today, this means multiple MCP tool calls per interaction — each hitting the database. At scale, this creates latency (multiple round-trips) and cost (redundant LLM token usage from re-fetching the same context).

Generic AI infrastructure solves this with session continuity and hot caches — keeping recently accessed context in memory for fast retrieval. HydraDB's "Composite Context Protocol" and Mem0's managed cloud service both address this pattern.

For Stratafy, the challenge is more specific: strategic context is hierarchical and role-dependent. A CEO needs the corporate strategy tree, key risks, and failing metrics. A product lead needs their functional strategy, linked initiatives, and relevant assumptions. The cache must be smart enough to pre-load the right context for the right person.

## The Approach

Build a strategic context cache that:

1. **Pre-assembles role-aware context bundles** — For each user role and workspace, maintain a pre-computed context package that includes the most relevant strategic entities
2. **Keeps hot context in memory** — Recently accessed entities and their relationships cached for sub-200ms retrieval
3. **Updates incrementally** — When an entity changes, invalidate and refresh only the affected cache entries, not the entire workspace
4. **Serves AI interactions** — Provide a single-call context endpoint that returns everything an AI agent needs for a given user + query type, replacing multiple sequential MCP calls

## Technical Design

- Redis or in-memory cache layer sitting between MCP tools and the database
- Context bundle schema: `{user_role, workspace_id, strategy_scope} → {strategies[], initiatives[], risks[], assumptions[], metrics[], recent_decisions[]}`
- Cache invalidation: event-driven — entity updates publish invalidation events, cache refreshes affected bundles
- Pre-warming: on user session start, pre-load their likely context bundle based on role and recent activity
- Token budget management: context bundles sized to fit within LLM context windows, with intelligent truncation that preserves the most strategically relevant content

## Success Criteria

- Context assembly time reduced from 3-5 seconds (multiple MCP calls) to under 200ms (single cache hit)
- Cache hit rate ≥ 80% for repeat interactions within a session
- Token usage per AI interaction reduced by 40%+ through smarter context assembly
- Zero stale data: cache invalidation ensures consistency within 1 second of any entity update

## Dependencies

- Requires Redis or equivalent in-memory store in the infrastructure stack
- Role-aware context assembly depends on team/role definitions being populated in workspaces
- Cache sizing needs production usage data to tune effectively
- Must not compromise data consistency — stale strategic context is worse than slow strategic context
