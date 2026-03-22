---
id: 7c85d506-7218-4c1e-984e-018fae24b311
type: initiative
status: in_progress
priority: high
strategy: Strategic AI Infrastructure
completionPercentage: 97
---

# Strategic Evolution & Time-Travel

## Description
Temporal strategy graph for tracking how strategy evolves over time. Infrastructure complete: daily snapshots with content hash deduplication, version-referenced content, field-level changelogs, content diffs, foundation diffing, git commit cross-referencing, AI narrative summaries, and causal chain detection. Now enriched with provenance: each auto-version carries a provenance_summary (which plugins, commands, actors, reasoning) and an LLM ai_assessment (magnitude, confidence, narrative, coherence). Remaining 3%: board reporting template and consumption-layer polish.

## Parent Strategy
[Strategic AI Infrastructure](../strategy/product/strategic-ai-infrastructure.md)

## Status & Progress
- **Status**: in progress
- **Priority**: high
- **Completion**: 97%

## Key Objectives
- [Causal chain detection: trace strategy changes to triggering assumptions/signals](../objectives/causal-chain-detection-trace-strategy-changes-to-triggering-assumptions-signals.md)

## Timeline
- **Start Date**: 2026-03-14
- **Target Date**: 2026-04-30

## Content
# Strategic Evolution & Time-Travel

## Status: 95% Infrastructure Complete (March 14, 2026)

All 6 phases shipped in one session. Infrastructure fully operational. Outstanding items are consumption-layer features built on top of the infrastructure.

---

## What's Built

### Phase 1: Snapshot Table & Daily Cron ✓
- `workspace_snapshots` table with YYYY.MM.DD.n versioning, content hash deduplication, change summaries
- Snapshot service: create, list, get, compare, batch processing
- Daily cron at 3 AM (`/api/_cron/snapshot`, Vercel `0 3 * * *`)
- Processes all active workspaces, skips unchanged via SHA-256 content hash

### Phase 2: Version-Referenced Architecture ✓
- `initiative_versions` table (mirrors strategy_versions)
- `trigger` column on strategy_versions ('published', 'auto_snapshot', 'manual')
- `content_diff` JSONB on both version tables (structured markdown section diffs)
- Auto-versioning: strategies/initiatives versioned when content hash changes
- Content stripped from snapshots, replaced with version_id references

### Phase 3: Temporal Query API ✓
- Entity history across snapshots (when was this entity added/modified/removed)
- Versioned content retrieval (strategy/initiative content at any point in time)
- Version timeline listing (all versions of a strategy/initiative)
- 3 API endpoints + 3 MCP tools

### Phase 4: Git Cross-Reference ✓
- Pre-sync snapshots created automatically before git push
- Commit SHA attached to snapshot after sync completes
- Non-blocking: snapshot failures don't prevent sync

### Phase 5: AI Narrative Analysis ✓
- grok-3-mini-fast-beta for cost-efficient summarization
- Lazy generation on first view, cached on `diff_analysis` + `diff_analyzed_at`
- Prompt assembles changelog + causal signals for strategic context
- API endpoint + MCP tool (analyze_snapshot)

### Phase 6: Causal Chain Detection ✓
- `getCausalSignals` query: given an entity, finds correlated changes in linked entities across recent snapshots
- Traverses assumption_contexts, risk_contexts, strategy_metric_links
- AI narrative enhanced with causal context for modified strategies
- API endpoint + MCP tool (get_causal_signals)

### Field-Level Changelog ✓
- Every structural change tracked with from/to values per entity
- Content version changes linked in changelog entries
- Foundation diffing: mission, vision, values, beliefs, principles
- Skips noisy fields (audit timestamps, hashes, summaries)

### Clean Baseline ✓
- First snapshot: 2026.03.14.1
- 43 strategies, 105 initiatives, 19 metrics, 31 assumptions, 21 risks, 23 decisions, 339 insights, 4 key priorities
- Foundation: mission, vision, 10 values, 32 beliefs, 16 principles
- 37 assumption-context links, 15 risk-context links, 16 strategy-metric links
- 42 strategy versions + 105 initiative versions with content diffs

---

## Totals

- **10 commits** shipped and pushed
- **12 MCP tools**: list_snapshots, get_snapshot, compare_snapshots, create_snapshot, get_entity_history, get_version_content, list_entity_versions, analyze_snapshot, get_causal_signals
- **9 API endpoints**: list, get, compare, create, entity-history, version-content, analyze, causal-signals
- **3 database tables**: workspace_snapshots (new), initiative_versions (new), strategy_versions (extended with trigger + content_diff)
- **1 daily cron**: 3 AM snapshot processing

---

## Outstanding Items

### Infrastructure Fixes (Small)

**1. Snapshot size optimization**
The test snapshot was 637KB because initiative descriptions are still inline in the snapshot JSON. `stripContentFromSnapshot` strips strategy content but keeps initiative descriptions. Fix: also strip initiative descriptions from the snapshot (keep only name, status, priority, completion_%, strategy_id, version_id). This brings snapshots to the target ~50-80KB range.

**2. Benchmark snapshot comparison performance**
`compareSnapshots` loads two full snapshot JSONBs and diffs in memory. Should be fast for 50-80KB snapshots but hasn't been benchmarked under production load. Verify <2 second claim.

### Consumption Layer (Product Features)

**3. Proactive causal alerting**
Currently pull-based: you ask "what caused this change?" via `get_causal_signals`. No push-based alerting exists. When an assumption's confidence changes from validated to invalidated, nothing proactively flags dependent strategies or decisions for review. Build: extend daily cron to detect high-impact causal correlations and surface them (via key priorities, insights, or notifications).

**4. Board reporting template**
The AI narrative generates 2-4 sentences. A proper quarterly strategy evolution report needs: strategy tree diff visualization, entity count trends, key assumption changes, initiative completion tracking, risk landscape shifts. Build: a `generate_evolution_report` MCP tool that assembles a structured report from multiple snapshots.

**5. Git commit link surfacing**
The `commit_sha` is stored on snapshot rows when sync triggers, but there's no user-facing "View this change in GitHub" link. Build: include `commit_url` (already on sync logs) and expose via MCP/API.

**6. Institutional memory onboarding**
No guided experience for new team members to browse strategic evolution. The data is available via MCP/API but there's no "show me how this strategy evolved from founding to now" flow. Build: a `get_strategy_evolution` MCP tool that assembles a narrative timeline for a specific strategy across all snapshots.

**7. Pattern analysis**
Temporal data accumulates daily but no aggregate analysis exists: how often does strategy change, which areas are most volatile, do assumptions tend to hold or get invalidated, do initiatives complete or quietly disappear. Build: aggregate queries across the snapshot timeline, surfaced as workspace health metrics.

**8. Snapshot size by workspace analytics**
No visibility into storage growth per workspace. Build: simple query on `workspace_snapshots` to track snapshot count, average size, and storage budget per workspace.

---

## Architecture

### Storage Model

```
workspace_snapshots (~50-80KB structural state, daily)
├── foundation: mission, vision, values, beliefs, principles (inline)
├── strategies: metadata + version_id reference (no content)
├── initiatives: metadata + version_id reference (no content/description)
├── small entities: inline (risks, assumptions, decisions, insights, metrics, objectives, key_priorities)
├── links: assumption_contexts, risk_contexts, strategy_metric_links
├── entity_counts + metadata
├── change_summary with field-level changelog + causal signals
├── diff_analysis (AI narrative, lazy cached)
└── commit_sha (git cross-reference)

strategy_versions (content changelog)
├── auto-created when content hash changes
├── trigger: 'published' | 'auto_snapshot' | 'manual'
├── content_diff: structured markdown section-level diffs
└── version_number matches snapshot version

initiative_versions (content changelog)
├── same pattern as strategy_versions
└── content_diff: structured section-level diffs
```

### Daily Cron Flow (3 AM)

```
for each active workspace:
  1. Generate snapshot via generateUnifiedSnapshot(trim: false)
  2. Compute content hash (SHA-256)
  3. Compare to last snapshot's hash → skip if unchanged
  4. For changed strategies/initiatives → auto-version with content_diff
  5. Strip content from snapshot, add version_id refs
  6. Compute field-level changelog against previous snapshot
  7. Save lightweight snapshot with changelog
```

### Sync Flow (Pre-sync hook)

```
on sync trigger:
  1. Create pre-sync snapshot (skipped if unchanged)
  2. Execute sync to destinations (GitHub, etc.)
  3. Attach commit_sha from successful sync result to snapshot
```

### Change Tracking Levels

1. **Entity counts** — quick "7 changes today"
2. **Field-level changelog** — which fields changed with from/to values
3. **Content diffs** — markdown section-level diffs on version rows
4. **AI narrative** — LLM-generated strategic summary with causal context (lazy, cached)
5. **Causal signals** — correlated changes in linked entities across snapshots

### Caching Strategy

- **Snapshots**: content hash deduplication — unchanged days produce no snapshot
- **AI narrative**: generated on first view, cached permanently (snapshot is immutable)
- **Content versions**: only created when content hash changes
- **Causal signals**: computed on demand (not cached — depends on growing snapshot history)

---

## Commits

| Commit | Phase | What |
|---|---|---|
| `4eb8e3de` | 1 | workspace_snapshots table, snapshot service, daily cron |
| `7937eb1a` | 2a | API endpoints, tool permissions, test count updates |
| `cd318269` | 2b | 4 MCP tools + removed pre-existing console.log issues |
| `9dcd0475` | 2c | initiative_versions, auto-versioning, lightweight snapshots |
| `4ec22134` | 2d | field-level changelog and content diffs |
| `496351b2` | 2e | foundation diffing in changelog |
| `67f91a02` | 3 | temporal query API (entity history, version content) |
| `c8577f0c` | 4 | git cross-reference (pre-sync snapshots ↔ commit SHA) |
| `b10c5878` | 5 | AI narrative analysis (grok-3-mini-fast-beta, lazy cached) |
| `f80cb6b4` | 6 | causal chain detection + enhanced AI narrative |

## Strategic Differentiation

This is the capability no generic AI infrastructure play can replicate. HydraDB's temporal graphs track data changes. Stratafy's snapshots track **strategic evolution** — typed relationships between strategies, initiatives, assumptions, and risks mean we answer "how has our strategy evolved?" not "what rows changed in the database?"

The version-referenced architecture means content evolution is a first-class concept. The causal chain detection means you can trace a strategy change back to the assumption invalidation that triggered it. The AI narrative means a board member gets "the GTM strategy shifted after the pricing assumption was invalidated" not "field status changed from active to archived on row 47."
