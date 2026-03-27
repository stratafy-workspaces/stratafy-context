---
id: 7c85d506-7218-4c1e-984e-018fae24b311
type: initiative
status: in_progress
priority: high
strategy: Strategic AI Infrastructure
completionPercentage: 98
---

# Strategic Evolution & Time-Travel

## Description
Temporal strategy graph for tracking how strategy evolves over time. Infrastructure complete: daily snapshots with content hash deduplication, version-referenced content, field-level changelogs, content diffs, foundation diffing, git commit cross-referencing, AI narrative summaries, and causal chain detection. Now enriched with provenance: each auto-version carries a provenance_summary (which plugins, commands, actors, reasoning) and an LLM ai_assessment (magnitude, confidence, narrative, coherence). Remaining 3%: board reporting template and consumption-layer polish.

## Parent Strategy
[Strategic AI Infrastructure](../strategy/product/strategic-ai-infrastructure.md)

## Status & Progress
- **Status**: in progress
- **Priority**: high
- **Completion**: 98%

## Key Objectives
- [Causal chain detection: trace strategy changes to triggering assumptions/signals](../objectives/causal-chain-detection-trace-strategy-changes-to-triggering-assumptions-signals.md)

## Timeline
- **Start Date**: 2026-03-14
- **Target Date**: 2026-04-30

## Content
# Strategic Evolution & Time-Travel

## Status: 98% Complete (March 22, 2026)

All 6 phases shipped. Consumption layer advancing — initiative detail page now has tabbed versions view, provenance records grouped under versions in History tab. Snapshot service refactored into focused modules.

## Recent Progress (Mar 15–22)

**Consumption Layer** — Initiative detail page now has a tabbed layout with versions API, bringing version history to the UI. Strategy History tab now groups provenance records under their corresponding versions.

**Code Quality** — Workspace snapshot service split into focused modules. Bug fix ensuring workspace_id is always set on auto-versioned records.

### Commits

| Commit | What |
|---|---|
| `b448882a` | Initiative tabbed detail page with versions API |
| `29c5e65b` | Group provenance records under versions in History tab |
| `074118e6` | Split workspace-snapshot-service into focused modules |
| `b509419d` | Fix: workspace_id always set on auto-versioned records |
| `3daccc4d` | Fix: await serverSupabaseServiceRole in snapshot filtering |

## What's Built

All 6 phases shipped: Snapshot Table & Daily Cron, Version-Referenced Architecture, Temporal Query API, Git Cross-Reference, AI Narrative Analysis, Causal Chain Detection, Field-Level Changelog, plus new Consumption Layer (initiative tabs, provenance under versions).

## Outstanding Items

1. Snapshot size optimization
2. Benchmark snapshot comparison performance
3. Proactive causal alerting
4. Board reporting template
5. Git commit link surfacing
6. Institutional memory onboarding
7. Pattern analysis
8. Snapshot size analytics

## Totals

- 12 MCP tools, 9 API endpoints, 3 database tables, 1 daily cron
