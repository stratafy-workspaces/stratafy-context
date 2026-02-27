---
id: d97fbeaa-7469-43ab-b6ba-fc44cff4ac5c
type: initiative
status: draft
priority: high
strategy: Product Architecture
completionPercentage: 0
lastUpdated: 2026-02-20T11:54:54.928646+00:00
owner: af04d126-d28a-43a7-be8b-0c9451873f1b
---

# Strategic Coherence Scan

## Description
Horizontal alignment scan that analyses all strategies in a workspace for coherence — detecting directional conflicts, resource tensions, reinforcement patterns, dependency gaps, and sequencing issues between strategies.

## Parent Strategy
[Product Architecture](../strategy/functional/product-architecture.md)

## Status & Progress
- **Status**: draft
- **Priority**: high
- **Completion**: 0%

## Key Objectives
No objectives defined

## Timeline
- **Start Date**: Not set
- **Target Date**: Not set

## Content
## Strategic Coherence Scan — Lens 2 of the Strategic Alignment Suite

### What It Does

The Strategic Coherence Scan is the horizontal alignment check — Strategy ↔ Strategy. While the Internal Alignment Scan (Lens 1) checks each strategy against foundation, the Coherence Scan checks whether the portfolio of strategic bets reinforces or undermines itself.

### Why It Matters

Each strategy looks reasonable in isolation. The danger is in the interactions:
- Two strategies competing for the same resources without acknowledgment
- Strategies pulling in opposite directions
- Strategy A assuming Strategy B delivers something B doesn't commit to
- Strategies that need sequencing but are treated as parallel

These tensions are invisible when strategies are reviewed one at a time. The Coherence Scan makes them visible.

### Architecture

Uses the existing `strategy_reviews` + `review_perspectives` tables:
- `strategy_reviews.review_type` = `'coherence_scan'`
- `strategy_reviews.strategy_id` = root strategy ID
- Each `review_perspective` = one finding (tension, reinforcement, gap, etc.)
- `perspective_type` values: `directional_conflict`, `resource_tension`, `reinforcement`, `dependency_gap`, `sequencing_issue`
- `supporting_data` JSON stores affected strategy IDs per finding

No new database tables needed — same schema as Internal Alignment, different review_type.

### Implementation

1. Fetch all strategies in workspace (with hierarchy, descriptions, status)
2. Fetch foundation context (mission, vision, values)
3. Fetch initiatives per strategy (resource demands)
4. Optionally fetch existing internal alignment scores
5. Build coherence prompt → call LLM → parse findings
6. Store as one `strategy_review` + N `review_perspective` rows
7. Expose via MCP tool (`run_coherence_scan`, `get_coherence_findings`)

### Part of the Strategic Alignment Suite

| Lens | Direction | Initiative |
|------|-----------|------------|
| 1. Internal Alignment | Vertical (Foundation ↔ Strategy) | Alignment Scan MVP (built) |
| **2. Strategic Coherence** | **Horizontal (Strategy ↔ Strategy)** | **This initiative** |
| 3. Radar Scanning | Inbound (External ↔ Strategy) | Radar MVP (separate) |
| 4. Public Presence | Outbound (Strategy ↔ External) | Public Narrative Alignment Scan |
| 5. Organizational | Structural (Strategy ↔ People) | Organigram-Strategy Alignment Scan |
