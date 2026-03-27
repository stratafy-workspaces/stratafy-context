---
id: ab8b9d04-baf2-41d5-89e4-509803b56572
type: initiative
status: active
priority: high
strategy: Strategic AI Infrastructure
completionPercentage: 5
---

# Context Consumption Analytics & Engagement Tracking

## Description
Track and visualize how strategic context is consumed across roles, plugins, and users. Every workspace snapshot request is logged with who, when, why, what role, how the context was filtered, original vs filtered size, and entity counts. This is the data layer that proves the role-aware context system is working and surfaces engagement signals (who's consuming strategy, who isn't, what's being ignored).

## Parent Strategy
[Strategic AI Infrastructure](../strategy/product/strategic-ai-infrastructure.md)

## Status & Progress
- **Status**: active
- **Priority**: high
- **Completion**: 5%

## Key Objectives
- [Proactive alerts for stale assumptions and strategic hygiene issues](../objectives/proactive-alerts-for-stale-assumptions-and-strategic-hygiene-issues.md)
- [Workspace health score calculated and visible for all active workspaces](../objectives/workspace-health-score-calculated-and-visible-for-all-active-workspaces.md)

## Timeline
- **Start Date**: 2026-03-24
- **Target Date**: 2026-05-31

## Content
# Context Consumption Analytics & Engagement Tracking

## Why Now

Context consumption is the most honest engagement signal in a strategic system. People don't lie about what they read. Every `get_workspace_snapshot` call is a moment where someone (or their AI agent) pulls strategic context to inform a decision. Tracking this gives us:

- **Who's engaged** — which team members, which expert plugins are consuming context
- **What they care about** — which strategies/sections get consumed vs ignored
- **Information asymmetry** — a CTO seeing 30K of context vs a team member seeing 8K
- **Consumption patterns** — daily rhythm vs sporadic, trending up vs declining
- **Optimization data** — which sections are always requested, where the payload is bloated

No other tool measures strategy consumption. This is a category-defining capability.

## Phases

### Phase 1: Logging Infrastructure (now)

Create `context_consumption_log` table, populated as a fire-and-forget side-effect in `get_workspace_snapshot` after filtering:

**Schema:**
- `id` (uuid)
- `workspace_id`
- `user_id` — who consumed
- `timestamp` — when
- `source_plugin` — which plugin triggered it (stratafy-team, stratafy-cto, etc.)
- `source_command` — which command (engage, call-it-a-day, etc.)
- `llm_reason` — why the AI pulled context
- `llm_intent` — user_request, autonomous, exploration, etc.
- `resolution_path` — expert_profile | user_profile | unfiltered
- `resolved_role` — the ws_role name that was resolved (ai_cto, null)
- `sections_requested` (jsonb) — ["strategies", "key_priorities"]
- `original_size_bytes` — pre-filter payload size
- `filtered_size_bytes` — post-filter payload size
- `compression_ratio` — filtered/original
- `entity_counts` (jsonb) — {strategies: 23, initiatives: 45, risks: 3, ...}
- `token_estimate` — rough token count of served context
- `context_hash` — hash of filtered payload for dedup/cache analysis

Optional (TTL 30 days):
- `filtered_context` (jsonb) — the actual served payload for analytics

**Implementation:** ~10 lines in the snapshot handler. Same fire-and-forget pattern as provenance logging.

### Phase 2: Frontend Dashboard (when data exists, ~2-3 weeks of accumulation)

`/ws/[id]/analytics/consumption` page showing:
- Timeline of consumption events by user/role
- Role breakdown — which expert roles consume most
- Compression heatmap — information asymmetry across roles
- Section popularity — which sections get requested
- Command patterns — which commands trigger context loading
- Engagement gaps — strategies never consumed (dead strategies)

### Phase 3: Intelligence (multi-user, Q3+)

- Drift detection: "CFO hasn't consumed financial strategy context in 14 days"
- Anomaly alerts: "Context consumption spiked 3x — someone's preparing"
- Optimization: "strategy_tree is 29K but only 3K used by team members"
- Cache strategy: "5 users pull same snapshot within 10 minutes daily — pre-compute"

## Relationship to Other Work

- **Validates assumption** `6f375c7d`: "Strategic engagement signals predict alignment gaps"
- **Feeds** Hot Strategic Context Cache — consumption patterns inform what to cache
- **Extends** Provenance Pipeline — provenance tracks mutations, this tracks reads
- **Enables** Pulse vision — consumption patterns ARE the pulse of an engagement

## Strategic Constraints

- Phase 1 logging must be zero-impact on snapshot latency (fire-and-forget)
- Never store filtered_context for workspaces that haven't opted in
- Consumption data is workspace-scoped — no cross-workspace analytics
- Build the log now, build the frontend when there's data worth showing
