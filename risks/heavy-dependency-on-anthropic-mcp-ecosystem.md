---
id: 93dc7f22-c6e2-4e81-8dfd-ab55a05e0b1b
type: risk
riskType: technical
riskSource: external
likelihood: low
impact: high
riskScore: 3
status: active
mitigationStatus: identified
lastUpdated: 2026-02-06T21:22:10.422789+00:00
---

# Heavy dependency on Anthropic/MCP ecosystem

## Description
Stratafy is deeply coupled to Anthropic's ecosystem — Claude as the AI backbone, MCP as the integration protocol, Claude Desktop as the primary interface. If Anthropic changes MCP spec, deprecates features, raises API pricing significantly, or a competitor's protocol wins (e.g., OpenAI's equivalent), Stratafy faces migration cost and potential architectural rework. Additionally, if MCP doesn't achieve broad adoption, the "plug into existing tools" value proposition weakens.

## Assessment
- **Likelihood**: low
- **Impact**: high
- **Risk Score**: 3
- **Type**: technical
- **Source**: external
- **Status**: active

## Mitigation
- **Status**: identified
- **Plan**: Abstract MCP integration behind an internal protocol layer so switching providers doesn't require full rewrite. Monitor MCP ecosystem adoption and competing protocols. Build REST API alongside MCP so the product isn't MCP-only. Maintain relationships with multiple AI providers. StratMD as an open format reduces single-vendor dependency on the content layer.
- **Review Date**: Not scheduled

