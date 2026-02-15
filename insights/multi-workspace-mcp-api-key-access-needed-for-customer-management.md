---
id: 8e89290f-0fe0-4e31-8f60-b1d290b43da3
type: insight
source: stratafy_chat
category: product
impactLevel: high
confidenceLevel: confirmed
status: pending
actionable: true
lastUpdated: 2026-02-10T10:59:05.699839+00:00
---

# Multi-workspace MCP API key access needed for customer management

## Summary
MCP API keys are scoped to single workspaces, blocking fluid movement between Stratafy and customer workspaces in Claude. Critical for scaling customer onboarding and the advisory firm use case.

## Description
When onboarding STIR Collective as first customer, we hit a blocker: the Claude AI MCP connector API key is scoped to a single workspace. This means Claude cannot switch between the Stratafy workspace and the STIR Collective workspace in the same session. The current workaround is creating a second MCP connector with a separate API key per workspace, but this doesn't scale.

As we onboard more customers, the founder (or any consultant/advisor using Stratafy) needs to move fluidly between workspaces — checking their own strategy, then switching to a client workspace to build theirs. This is especially critical for the advisory firm use case where one person manages multiple client workspaces.

Required capability: MCP API keys that can access multiple workspaces, with select_workspace toggling between them. The workspace list should show all workspaces the user has access to, not just the one the key is scoped to.

This directly impacts the Advisory Firms GTM channel — coaches and advisors need cross-workspace access as a core workflow.

## Classification
- **Source**: stratafy chat
- **Category**: product
- **Impact**: high
- **Confidence**: confirmed
- **Status**: pending
- **Actionable**: Yes
- **Tags**: mcp, multi-workspace, api-key, customer-onboarding, advisory-firms, product-gap, first-customer-learning


