---
id: 64cdab1d-f203-4bbb-96da-8cddf38f83b7
type: decision
decisionType: type_2_reversible
status: decided
decidedAt: 2026-01-30T15:18:14.362+00:00
lastUpdated: 2026-01-30T15:18:14.656693+00:00
---

# Radar Output Structuring with Auto-Insight Creation

## Description
How should we structure Radar scan outputs for MCP consumption and Insights integration? The existing Radar layer stores results as unstructured JSON in `radar_executions.result`. We need structured data for Claude to interact with Radar directly and to feed the learning loop.

## Details
- **Type**: Type 2 (Reversible)
- **Status**: decided
- **Authority**: Technical Director / Founder
- **Deadline**: No deadline
- **Decided At**: 2026-01-30T15:18:14.362+00:00

## Context
Existing infrastructure: Full `layers/radar/` with sessions, prompts, executions. Insights system has `source: 'stratafy_radar'` enum. No MCP tools for Radar currently exist. Strategic Intelligence strategy specifies Radar as external sensing capability with Phase 1 prototype functional.

## Research
No research recorded

## Decision
Add three new tables to structure Radar output: `radar_findings` (individual signals), `radar_implications` (linked to strategies), and `radar_recommendations` (actionable items). Findings auto-create Insights with `source: 'stratafy_radar'`. Add MCP tools for full CRUD operations. This enhances the existing Radar layer rather than replacing it.

## Rationale
1. **Enables MCP integration** — Claude can interact with structured findings, not raw JSON blobs
2. **Feeds the learning loop** — Auto-insight creation ensures Radar findings flow into the unified Insights system
3. **Creates cold-start moat** — Structured findings compound over time, creating switching cost
4. **Links external to internal** — Implications connect external signals to specific strategies
5. **Follows proven pattern** — Same MCP-first, dogfood-before-UI approach as Decision Log
6. **Minimal risk** — Type 2 decision; schema can evolve based on dogfooding feedback

## Outcome
No outcome recorded yet
