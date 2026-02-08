---
id: dd2ae1a0-bcc5-4baf-a181-d5ed699dbfea
type: insight
source: stratafy_chat
category: product
impactLevel: high
confidenceLevel: confirmed
status: processed
actionable: true
lastUpdated: 2026-02-06T08:19:02.301078+00:00
---

# Stratafy metrics framework — platform health + workspace engagement

## Summary
Core metrics: workspaces (total, active), users (total, active, DAU/WAU/MAU), usage stats (calls, MCP ratio, errors), strategies per workspace, foundation completeness. Split into admin dashboard (platform) and workspace dashboard (per customer).

## Description
## Platform Health Metrics (Admin Dashboard)

Cross-workspace metrics for Stratafy as a business:

| Metric | Query | Purpose |
|--------|-------|---------|
| **Total Workspaces** | `COUNT(*) FROM workspaces WHERE deleted_at IS NULL` | Platform scale |
| **Active Workspaces** | Workspaces with activity in last 30 days | Engagement health |
| **Total Users** | `COUNT(*) FROM users WHERE deleted_at IS NULL` | User base size |
| **Active Users** | Users with activity in last 7/30 days (DAU, WAU, MAU) | Engagement depth |
| **Users per Workspace** | Average, median, distribution | Org size patterns |

## Usage Metrics (from usage_events)

| Metric | Query | Purpose |
|--------|-------|---------|
| **Total API Calls** | Count by day/week/month | Volume trend |
| **MCP vs UI Ratio** | source breakdown | AI consumption proof |
| **Calls per Workspace** | Average, distribution | Engagement intensity |
| **Error Rate** | result_status = 'error' / total | Platform reliability |
| **Avg Response Time** | AVG(duration_ms) by operation | Performance |

## Workspace Engagement Metrics (Per-Workspace Dashboard)

Content depth indicators:

| Metric | Query | Target | Purpose |
|--------|-------|--------|---------|
| **Foundation Completeness** | Has mission + vision + ≥3 values + ≥1 belief + ≥1 principle | 100% | Setup health |
| **Strategy Count** | strategies per workspace | ≥5 | Strategic depth |
| **Strategy Tree Depth** | Max parent-child levels | ≥2 | Hierarchy usage |
| **Initiative Count** | initiatives per workspace | ≥3 | Execution connection |
| **Insight Count** | insights captured | Growing | Feedback loop active |
| **Insight Processing Rate** | processed / total insights | >50% | Loop closing |

## Derived Health Scores

| Score | Formula | Purpose |
|-------|---------|---------|
| **Workspace Health** | Weighted: foundation (30%) + strategies (30%) + activity (40%) | At-a-glance engagement |
| **AI Adoption** | MCP calls / total calls | Thesis validation |
| **Feedback Loop Active** | Insights created + processed in last 7 days > 0 | Core value delivery |

## Dashboard Views Needed

1. **Admin Dashboard** (Stratafy internal): All platform metrics, all workspaces
2. **Workspace Dashboard** (Per customer): Their metrics, their usage, their health scores
3. **Usage Analytics** (Detailed): The MCP/UI breakdown, tool usage, client distribution

## Classification
- **Source**: stratafy chat
- **Category**: product
- **Impact**: high
- **Confidence**: confirmed
- **Status**: processed
- **Actionable**: Yes
- **Tags**: metrics, dashboard, platform, engagement, analytics


