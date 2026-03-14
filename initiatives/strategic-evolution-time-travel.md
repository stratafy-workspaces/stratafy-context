---
id: 7c85d506-7218-4c1e-984e-018fae24b311
type: initiative
status: in_progress
priority: high
strategy: Strategic AI Infrastructure
completionPercentage: 60
---

# Strategic Evolution & Time-Travel

## Description
Build a temporal strategy graph that captures how strategy evolves over time. Capabilities: snapshot entire strategy tree at any point, compare snapshots ("strategy diff"), track when strategies/initiatives were added/removed/modified, surface assumption changes that drove pivots. Answers the board question: "How has our strategy evolved since last quarter?" No generic AI infrastructure play can do this because they don't know what strategy is.

## Parent Strategy
[Strategic AI Infrastructure](../strategy/product/strategic-ai-infrastructure.md)

## Status & Progress
- **Status**: in progress
- **Priority**: high
- **Completion**: 60%

## Key Objectives
- [Causal chain detection: trace strategy changes to triggering assumptions/signals](../objectives/causal-chain-detection-trace-strategy-changes-to-triggering-assumptions-signals.md)
- [AI-generated strategic change narratives (lazy-cached)](../objectives/ai-generated-strategic-change-narratives-lazy-cached.md)
- [Strategic diff with field-level changelog and content diffs](../objectives/strategic-diff-with-field-level-changelog-and-content-diffs.md)
- [Point-in-time workspace snapshot retrieval in under 2 seconds](../objectives/point-in-time-workspace-snapshot-retrieval-in-under-2-seconds.md)

## Timeline
- **Start Date**: Not set
- **Target Date**: 2026-09-30

## Content
# Strategic Evolution & Time-Travel

## Current Status (March 2026)

~60% built. Phase 1 and Phase 2 complete. Clean baseline snapshot live with 630+ entities, foundation data, version-referenced content, field-level changelog, and content diffs.

### What's Built

#### Infrastructure (Pre-existing)
- `strategy_versions` table with version_number, changelog, content, strategy_details, published_at
- `unified-snapshot-service.ts` — complete workspace state in a single call
- `change-detection-service.ts` — SHA-based change detection with compareManifests
- GitHub sync with daily/weekly/monthly scheduling, commit SHAs, markdown export
- Distillation cron (every 5 min) with SHA-256 content hashing on every entity

#### Phase 1 — Complete (March 14, 2026)
- `workspace_snapshots` table with version numbering (YYYY.MM.DD.n), content hash deduplication, change summaries
- Snapshot service: create, list, get, compare, batch processing
- Daily cron at 3 AM (`/api/_cron/snapshot`) — processes all workspaces, skips unchanged
- Vercel cron configuration (`0 3 * * *`)

#### Phase 2 — Complete (March 14, 2026)

**2a. API & MCP Tools**
- API endpoints: GET list, GET by ID, GET compare, POST create
- MCP tools: list_snapshots, get_snapshot, compare_snapshots, create_snapshot
- Tool permissions (strategy:read for queries, strategy:write for create)

**2b. Version-Referenced Architecture**
- `initiative_versions` table (mirrors strategy_versions pattern)
- `trigger` column on strategy_versions ('published', 'auto_snapshot', 'manual')
- Auto-versioning: strategies/initiatives versioned when content hash changes during snapshot
- Content stripped from snapshot JSON, replaced with version_id references
- Content diffs computed and stored on version rows (`content_diff` JSONB)

**2c. Field-Level Changelog**
- Every structural change tracked with from/to values per entity
- Content version changes linked in changelog entries
- Foundation diffing: mission, vision, values, beliefs, principles all tracked
- Four levels of change detail:
  1. Entity counts — quick scan ("7 changes today")
  2. Field-level changelog — which fields changed with from/to values
  3. Content diffs — markdown section-level diffs on version rows
  4. AI narrative (future, lazy) — LLM-generated summary

**2d. Clean Baseline**
- First snapshot: version 2026.03.14.1
- 43 strategies, 105 initiatives, 19 metrics, 31 assumptions, 21 risks, 23 decisions, 339 insights, 4 key priorities
- Foundation: mission, vision, 10 values, 32 beliefs, 16 principles
- Relationships: 37 assumption-context links, 15 risk-context links, 16 strategy-metric links
- 42 strategy versions + 105 initiative versions created with content diffs

### What's Remaining

#### Phase 3: Temporal Query API (~1-2 days)
- `GET /ws/:id/snapshots/entity/:entityId/history` — entity across snapshots
- `GET /ws/:id/snapshots/:id/strategy/:strategyId/content` — load versioned content
- MCP tools: get_entity_history, get_snapshot_content
- Version diff endpoint: compare two versions of a strategy/initiative

#### Phase 4: Git Cross-Reference (~0.5 days)
- Link snapshot rows to git commits via commit_sha
- When sync runs, save snapshot first, attach commit SHA
- MCP: "View this change in GitHub"

#### Phase 5: AI Narrative (Lazy, Cached)
- On first view of snapshot diff, assemble structural changes + content diffs
- Send to LLM: "Summarize what changed strategically"
- Cache on `diff_analysis` field, set `diff_analyzed_at`
- Uses distillation model (Grok 3 mini) to keep cost low

#### Phase 6: Causal Chain Detection (Future)
- When assumption confidence changes, flag dependent decisions for review
- When strategy is modified, log which assumption/signal/insight changes preceded it
- "What assumption changed that caused this pivot?" as queryable relationship

---

## Architecture

### Storage Model

```
workspace_snapshots (~50-80KB structural state)
├── foundation: mission, vision, values, beliefs, principles (inline)
├── strategies: metadata + version_id reference (no content)
├── initiatives: metadata + version_id reference (no content/description)
├── small entities: inline (risks, assumptions, decisions, insights, metrics, objectives, key_priorities)
├── links: assumption_contexts, risk_contexts, strategy_metric_links
├── entity_counts + metadata.diagnostics
└── change_summary with field-level changelog

strategy_versions (content changelog)
├── auto-created when content hash changes
├── trigger: 'published' | 'auto_snapshot' | 'manual'
├── content_diff: structured markdown section-level diffs
└── version_number matches snapshot version

initiative_versions (content changelog)
├── same pattern as strategy_versions
├── content_diff: structured section-level diffs
└── tracks content + description evolution
```

### Daily Cron Flow

```
3 AM → for each active workspace:
  1. Generate snapshot via generateUnifiedSnapshot(trim: false)
  2. Compute content hash
  3. Compare to last snapshot's hash → skip if unchanged
  4. For changed strategies/initiatives → auto-version with content_diff
  5. Strip content from snapshot, add version_id refs
  6. Compute field-level changelog against previous snapshot
  7. Save lightweight snapshot with changelog
```

### Change Tracking Levels

1. **Entity counts** — `entity_counts` JSONB: quick "7 changes today"
2. **Field-level changelog** — `change_summary.changelog[]`: which fields changed on which entities, from/to values, content version references
3. **Content diffs** — `content_diff` on version rows: sections added/removed/modified, line counts, significant changes
4. **AI narrative** — `diff_analysis` on snapshot: LLM-generated strategic summary (lazy, cached on first view)

### Version Numbering
- `YYYY.MM.DD.n` — date-based, human-readable, sortable
- `.n` auto-increments for same-day snapshots (daily cron + manual/milestone)
- Matches across snapshot and version tables

---

## Commits

| Commit | What |
|---|---|
| `4eb8e3de` | Phase 1: workspace_snapshots table, snapshot service, daily cron |
| `7937eb1a` | Phase 2a: API endpoints, tool permissions, test count updates |
| `cd318269` | Phase 2b: 4 MCP tools + removed pre-existing console.log issues |
| `9dcd0475` | Phase 2c: initiative_versions, auto-versioning, lightweight snapshots |
| `4ec22134` | Phase 2d: field-level changelog and content diffs |
| `496351b2` | Phase 2e: foundation diffing in changelog |

## Strategic Differentiation

No generic AI infrastructure play can replicate this. The version-referenced architecture means content evolution is a first-class concept. You can trace a strategy's thinking from v1 through v15, see the changelog at each step, correlate content changes with structural changes, and eventually ask "what assumption changed that caused this pivot?" — all from typed strategic relationships, not generic data changes.
