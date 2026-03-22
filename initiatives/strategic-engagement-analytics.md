---
id: ab8b9d04-baf2-41d5-89e4-509803b56572
type: initiative
status: draft
priority: medium
strategy: Strategic AI Infrastructure
completionPercentage: 0
---

# Strategic Engagement Analytics

## Description
Deferred to Phase 3. Track strategic engagement patterns (who queries what, when engagement drops, content health scoring) and feed into proactive drift detection. Will build when there are enough active workspaces to generate meaningful engagement data. Strategy-level health scores already exist as a foundation.

## Parent Strategy
[Strategic AI Infrastructure](../strategy/product/strategic-ai-infrastructure.md)

## Status & Progress
- **Status**: draft
- **Priority**: medium
- **Completion**: 0%

## Key Objectives
- [Proactive alerts for stale assumptions and strategic hygiene issues](../objectives/proactive-alerts-for-stale-assumptions-and-strategic-hygiene-issues.md)
- [Workspace health score calculated and visible for all active workspaces](../objectives/workspace-health-score-calculated-and-visible-for-all-active-workspaces.md)

## Timeline
- **Start Date**: Not set
- **Target Date**: 2026-09-30

## Content
# Strategic Engagement Analytics

## The Problem

Stratafy captures strategic architecture — but doesn't yet measure how that architecture is being used. We don't know: Which strategies are being queried most? Which assumptions haven't been reviewed in 6 months? Which teams are actively engaging with their objectives vs. ignoring them? Which insights are being generated but never acted on?

This is a gap that generic AI infrastructure doesn't even attempt to fill, because it requires domain knowledge about what "strategic engagement" means. It's not about DAU or session length — it's about whether the strategy is actually governing decisions.

## The Approach

Build an analytics layer that tracks strategic engagement across two dimensions:

1. **Content health** — Is the strategic architecture complete, current, and well-formed?
   - Strategies without initiatives (intent without action)
   - Initiatives without objectives (action without measurement)
   - Assumptions that haven't been reviewed in 90+ days
   - Risks without mitigation plans
   - Metrics without recent data points

2. **Usage patterns** — Is the team actually using the strategy to make decisions?
   - Which entities are being queried/viewed/updated most frequently
   - Decision → strategy traceability: are decisions referencing the strategy?
   - Insight generation rate: is the feedback loop active?
   - Time between insight creation and strategy adjustment
   - Cross-team engagement: which teams are strategically active vs. dormant

## Technical Design

- Event tracking: log all entity interactions (view, query, update, create, link) with user, timestamp, and context
- Health scoring: automated scoring for each workspace based on completeness, freshness, and structural integrity
- Engagement dashboards: workspace-level and team-level views showing strategic engagement metrics
- Alerting: proactive notifications when engagement drops (e.g., "Your GTM strategy hasn't been reviewed in 30 days") or health degrades (e.g., "3 high-impact assumptions are overdue for validation")
- Benchmarking: aggregate anonymous engagement data across workspaces to establish "what good looks like"

## Success Criteria

- Workspace health score calculated and visible for all active workspaces
- At least 5 engagement metrics tracked and trended over time
- Proactive alerts for strategic hygiene issues (stale assumptions, unmeasured initiatives, orphaned risks)
- Board-ready engagement reports showing strategy adoption across teams
- Measurable correlation between engagement scores and strategic execution quality

## Dependencies

- Requires event logging infrastructure across all MCP tools and UI interactions
- Privacy considerations: engagement data must be aggregated, not used for individual surveillance
- Needs baseline data from production workspaces to calibrate health scores and alerting thresholds
- UI design for dashboards and health score visualisation
