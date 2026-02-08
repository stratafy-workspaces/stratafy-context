---
id: db593741-32e9-4a18-b574-581145739a8b
type: risk
riskType: technical
riskSource: internal
likelihood: high
impact: high
riskScore: 9
status: active
mitigationStatus: identified
lastUpdated: 2026-02-06T21:21:46.916349+00:00
---

# MCP-first architecture limits demo accessibility

## Description
Shipping MCP-first without UI means the product can only be experienced through Claude Desktop or similar MCP clients. This limits who can demo and evaluate Stratafy — investors, prospects, and lighthouse customers need technical setup to experience the product. ScaleUp Company, Pieter, and Sequoia may not have Claude Desktop configured. The "demo is the product" principle breaks if the demo requires tooling the prospect doesn't have.

## Assessment
- **Likelihood**: high
- **Impact**: high
- **Risk Score**: 9
- **Type**: technical
- **Source**: internal
- **Status**: active

## Mitigation
- **Status**: identified
- **Plan**: Prioritize web UI for Alignment Scan and core workflows before lighthouse demos. Create a hosted demo mode that doesn't require MCP setup. Prepare screen-share demo flow as interim fallback. Consider building a lightweight web chat interface that wraps MCP calls.
- **Review Date**: Not scheduled

