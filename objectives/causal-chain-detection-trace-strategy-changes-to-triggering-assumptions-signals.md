---
id: 1c7b05ea-3615-4400-9191-0909d93339b4
type: objective
objectiveType: key_result
status: active
priority: high
initiative: Strategic Evolution & Time-Travel
---

# Causal chain detection: trace strategy changes to triggering assumptions/signals

## Description
When a strategy or initiative is modified, the system can trace backward to identify which assumption confidence change, signal, or insight preceded and likely triggered the change. Phase 6 shipped the core infrastructure: getCausalSignals traverses typed relationships (assumption_contexts, risk_contexts, strategy_metric_links) to find correlated changes across recent snapshots. AI narrative is enhanced with causal context. Remaining gap: proactive alerting — currently pull-based only. No cron-triggered flagging when a high-impact causal correlation is detected. This needs real usage data to validate query patterns before building.

## Hierarchy
**Strategy**: [Strategic AI Infrastructure](../strategy/product/strategic-ai-infrastructure.md)
**Initiative**: [Strategic Evolution & Time-Travel](../initiatives/strategic-evolution-time-travel.md)

## Objective Details
- **Type**: key result
- **Status**: active
- **Priority**: high
- **Target Value**: Query API that traces strategy changes to triggering assumptions/signals/insights
- **Current Value**: Infrastructure built — getCausalSignals query traces changes across assumption_contexts, risk_contexts, strategy_metric_links. MCP tool + API endpoint live. AI narrative enhanced with causal context. Remaining: proactive alerting (cron-triggered flagging when high-impact causal correlations detected).

## OKR Scoring
No OKR score set

## Timeline
- **Target Date**: 2026-07-31

## Content
No content available
