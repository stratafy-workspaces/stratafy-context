---
id: b372f5cf-d322-4ba1-86e9-be3aea561803
type: initiative
status: in_progress
priority: high
strategy: Product-Market Fit
completionPercentage: 0
lastUpdated: 2026-02-11T09:39:57.75+00:00
owner: af04d126-d28a-43a7-be8b-0c9451873f1b
---

# Platform & Usage Analytics Dashboard

## Description
Build comprehensive analytics dashboards for Stratafy. Two views: (1) Admin Dashboard — platform health metrics including total/active workspaces, total/active users, DAU/WAU/MAU, usage volume, error rates; (2) Usage Analytics — MCP vs UI ratio, human-AI collaboration, tool adoption, client distribution. This is operational infrastructure AND proof points for the thesis. Instrumentation deployed Jan 27, 2026.

## Parent Strategy
[Product-Market Fit](../strategy/functional/product-market-fit.md)

## Status & Progress
- **Status**: in progress
- **Priority**: high
- **Completion**: 0%

## Key Objectives
No objectives defined

## Timeline
- **Start Date**: 2026-01-27
- **Target Date**: 2026-02-21

## Content
# Platform & Usage Analytics Dashboard

## Purpose

Build the analytics infrastructure that:
1. Runs the business (platform health visibility)
2. Proves the thesis (MCP adoption trending up)
3. Demonstrates customer value (workspace engagement)

## Dashboard 1: Admin Dashboard (Internal)

Platform-wide metrics for running Stratafy as a business.

### Key Metrics

| Metric | Source | Display |
|--------|--------|---------|
| Total Workspaces | `workspaces` table | Number card |
| Active Workspaces (30d) | `usage_events` joined | Number card + trend |
| Total Users | `users` table | Number card |
| Active Users (DAU/WAU/MAU) | `usage_events` | Number cards + trend |
| Users per Workspace | Derived | Distribution chart |

### Workspace Table

List all workspaces with:
- Name
- Created date
- User count
- Strategy count
- Last activity
- Health score (derived)

Click through to workspace detail.

## Dashboard 2: Usage Analytics

The proof-point dashboard for investors and thesis validation.

### Hero Metric: MCP vs UI Ratio

```
┌─────────────────────────────────────────┐
│  MCP Usage: 68%  ████████████████░░░░░  │
│  UI Usage:  32%  ████████░░░░░░░░░░░░░  │
└─────────────────────────────────────────┘
```

Target: MCP grows to 70%+ over time.

### Charts

1. **MCP vs UI Over Time** (area chart, stacked)
   - X: Date
   - Y: Call count
   - Series: MCP, UI

2. **Tool Usage Ranking** (horizontal bar)
   - Top 10 MCP tools by call count
   - Shows which capabilities AI agents use most

3. **Client Distribution** (pie/donut)
   - Claude Desktop vs Claude Code vs Cursor vs Other
   - Proves ecosystem breadth

4. **Human vs AI Activity** (area chart)
   - Sessions with user_id only
   - Sessions with agent_id only
   - Sessions with both (collaboration)

5. **Error Rate Trend** (line chart)
   - Target: <5%
   - Alert if trending up

### Filters

- Time range: 7d / 30d / 90d / All time
- Workspace: All / Specific workspace
- Source: All / MCP / UI / API

## Dashboard 3: Workspace Engagement (Per-Customer)

What customers see about their own workspace.

### Metrics

| Metric | Target | Display |
|--------|--------|---------|
| Foundation Completeness | 100% | Progress bar |
| Strategy Count | ≥5 | Number + trend |
| Initiative Count | ≥3 | Number + trend |
| Insight Count | Growing | Number + trend |
| Insight Processing Rate | >50% | Percentage |
| MCP Usage | Growing | Trend chart |

### Health Score

Composite score (1-100):
- Foundation: 30%
- Strategies: 30%
- Activity: 40%

Displayed as gauge or grade (A/B/C/D).

## Technical Implementation

### Data Sources

1. `workspaces` — workspace metadata
2. `users` — user accounts
3. `workspace_members` — user-workspace relationships
4. `strategies` — strategy count per workspace
5. `initiatives` — initiative count per workspace
6. `insights` — insight count, processing status
7. `usage_events` — all activity tracking (NEW)
8. Foundation tables — mission, vision, values, beliefs, principles

### Queries (Core)

```sql
-- Active workspaces (30d)
SELECT COUNT(DISTINCT workspace_id)
FROM usage_events
WHERE created_at > NOW() - INTERVAL '30 days';

-- MCP vs UI ratio
SELECT source, COUNT(*) as calls
FROM usage_events
WHERE created_at > NOW() - INTERVAL '7 days'
GROUP BY source;

-- Tool usage ranking
SELECT mcp_tool_name, COUNT(*) as calls
FROM usage_events
WHERE source = 'mcp'
GROUP BY mcp_tool_name
ORDER BY calls DESC
LIMIT 10;

-- DAU
SELECT DATE(created_at) as day, COUNT(DISTINCT user_id) as dau
FROM usage_events
WHERE user_id IS NOT NULL
GROUP BY day
ORDER BY day DESC;
```

### Routes

- `/admin/dashboard` — Platform health (admin only)
- `/admin/usage` — Usage analytics (admin only)
- `/ws/[id]/dashboard` — Workspace engagement (workspace members)

## Scope

### Phase 1 (Feb 15)

- [ ] Admin dashboard with key platform metrics
- [ ] Usage analytics with MCP vs UI chart
- [ ] Basic workspace engagement view

### Phase 2 (Post-MVP)

- [ ] Health scores and alerts
- [ ] Export/reporting
- [ ] Customer-facing engagement dashboard
- [ ] Automated insights from metrics

## Success Criteria

- Can answer "how many active users do we have?" in <5 seconds
- Can show MCP adoption trend to investors
- Can identify disengaged workspaces for outreach
- Error rate visible and <5%
