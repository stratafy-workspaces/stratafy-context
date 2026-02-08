---
id: d9c75c43-c9d6-4a49-881c-73a973e7bc88
type: insight
source: stratafy_chat
category: product
impactLevel: high
confidenceLevel: likely
status: pending
actionable: true
lastUpdated: 2026-02-08T09:18:46.236991+00:00
---

# Workspace hierarchy (parent/child) required for VC and advisory use cases

## Summary
Flat workspace structure breaks the VC and advisory firm value propositions. VCs need their own strategy PLUS cross-portfolio visibility. Requires parent/child workspace hierarchy with cross-workspace querying and role-appropriate access.

## Description
Current workspace architecture is flat — every workspace is independent. But the VC use case requires hierarchy: Sequoia has its own strategy AND visibility into portfolio company workspaces. A VC partner asking "which portfolio companies have the highest strategic drift?" needs to query across child workspaces. This is also true for advisory firms — ScaleUp Company needs their own workspace plus visibility into client workspaces. The pattern is: parent workspace (aggregator) with child workspaces (companies), where the parent can query across children with appropriate permissions. This is the portfolio visibility feature that makes the VC and advisory firm channels work. Without it, each workspace is an island.

## Classification
- **Source**: stratafy chat
- **Category**: product
- **Impact**: high
- **Confidence**: likely
- **Status**: pending
- **Actionable**: Yes
- **Tags**: workspace-architecture, vc-use-case, advisory-use-case, portfolio-visibility, hierarchy


