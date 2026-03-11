---
id: 9ffe02c3-67cb-401a-a39b-9d361d6d8208
type: insight
source: stratafy_chat
category: product
impactLevel: medium
confidenceLevel: confirmed
status: processed
actionable: true
---

# Unified document generation engine — investor updates and strategy exports share 80% infrastructure, already validated via MCP

## Summary
Investor Update Generator and Strategy Export share 80% infra. Full investor update already validated from existing MCP tools. Build a generic document generation engine with template types, investor update as first template.

## Description
SYNTHESIZED FROM 2 INSIGHTS (Feb 8, 2026): 98cb024b, 4cf7f605

Investor Update Generator and Strategy Export share ~80% infrastructure: workspace snapshot → structured data extraction → template application → formatted output. Building one makes the other incremental.

VALIDATED: Full investor update was generated from existing MCP tools (get_workspace_snapshot, list_metrics, list_risks, list_assumptions, list_decisions). Only human input needed was narrative framing. The data layer is already sufficient.

ARCHITECTURE: Build a generic workspace document generation engine with template types (investor update, strategy one-pager, board pack, alignment report) rather than two separate features. Engine takes template type + date range, pulls changes, structures into template, outputs markdown/PDF.

IMPLEMENTATION: Build shared engine with investor update as first template, then add PDF export templates incrementally. Period-over-period metric comparison comes free from current_value vs previous_value fields.

## Classification
- **Source**: stratafy chat
- **Category**: product
- **Impact**: medium
- **Confidence**: confirmed
- **Status**: processed
- **Actionable**: Yes
- **Tags**: synthesized, document-generation, investor-update, strategy-export, mcp, architecture


