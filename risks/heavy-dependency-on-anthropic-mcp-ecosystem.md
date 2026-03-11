---
id: 93dc7f22-c6e2-4e81-8dfd-ab55a05e0b1b
type: risk
riskType: technical
riskSource: external
likelihood: low
impact: high
riskScore: 3
status: active
mitigationStatus: in_progress
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
- **Status**: in_progress
- **Plan**: Multi-Platform Strategic Access strategy (Chat SDK) ensures Stratafy's value persists across Slack, Google Chat, Teams, Discord, Telegram, Linear, and GitHub — independent of Anthropic's ecosystem. Google Chat already working, Telegram in testing. Claude remains the deepest interface but is no longer the only path to strategic intelligence. Additionally, Stratafy's API-first architecture means any AI provider can consume the strategic context via MCP or direct API.
- **Review Date**: Not scheduled

