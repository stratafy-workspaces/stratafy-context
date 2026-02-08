---
id: b3975639-08cb-4e01-adf0-eed4ae4d72f1
type: insight
source: stratafy_chat
category: product
impactLevel: high
confidenceLevel: confirmed
status: processed
actionable: true
lastUpdated: 2026-02-06T08:19:08.975798+00:00
---

# Usage metrics spec — MCP ratio as primary proof point

## Summary
Key metrics from usage_events: MCP/UI ratio (target: MCP dominance over time), human-AI collaboration index, tool adoption curve, client distribution. Instrumentation live Jan 27, 2026.

## Description
## Core Metrics (from usage_events table)

**1. MCP vs UI Ratio**
- Query: `source = 'mcp'` vs `source = 'ui'` calls
- Target: MCP grows to 70%+ of total usage
- Why it matters: Proves strategy is AI-consumed infrastructure, not just human-readable docs

**2. Human-AI Collaboration Index**
- Query: Sessions with both `user_id` AND `agent_id` activity
- Target: Increasing collaboration sessions per week
- Why it matters: Proves symbiosis thesis — AI amplifies, doesn't replace

**3. MCP Calls per Day (Growth)**
- Query: Daily count where `source = 'mcp'`
- Target: Week-over-week growth
- Why it matters: Raw adoption signal for AI consumption

**4. Tool Adoption Curve**
- Query: `mcp_tool_name` ranked by calls over time
- Target: Strategy/foundation tools most used
- Why it matters: Shows which capabilities AI agents find valuable

**5. MCP Client Distribution**
- Query: `mcp_client_name` breakdown (Claude Desktop, Claude Code, Cursor)
- Target: Multi-client adoption
- Why it matters: Proves ecosystem breadth, not single-client dependency

**6. Error Rate by Tool**
- Query: `result_status = 'error'` / total by `mcp_tool_name`
- Target: <5% error rate
- Why it matters: Operational health, reliability for AI consumers

## Pitch Story Arc
- Week 1: Mostly UI (human setup)
- Week 4: MCP overtakes UI (AI doing work)
- Week 8: 70%+ MCP (strategy = AI infrastructure)

## Data Available
- workspace_id, source, operation, operation_category
- user_id/email (human), agent_id/name (AI)
- mcp_tool_name, mcp_auth_mode, mcp_session_id, mcp_client_name
- result_status, duration_ms, created_at

## Classification
- **Source**: stratafy chat
- **Category**: product
- **Impact**: high
- **Confidence**: confirmed
- **Status**: processed
- **Actionable**: Yes
- **Tags**: metrics, MCP, usage, analytics, proof-point, pitch


