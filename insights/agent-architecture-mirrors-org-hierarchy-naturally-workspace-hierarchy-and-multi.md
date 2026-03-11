---
id: 0420b068-5898-4c41-8949-0e264d9d393f
type: insight
source: stratafy_chat
category: product
impactLevel: high
confidenceLevel: likely
status: processed
actionable: true
---

# Agent architecture mirrors org hierarchy naturally — workspace hierarchy and multi-workspace access are critical blockers for VC and advisory channels

## Summary
Agent roles naturally stratify like org hierarchy (orchestrator, creator, reviewer, automator). Every agent deployed = triple win (leverage + validation + narrative). Two critical platform gaps: workspace parent/child hierarchy needed for VC/advisory portfolio visibility, and multi-workspace MCP API access needed for customer management at scale.

## Description
SYNTHESIZED FROM 4 INSIGHTS (Feb 8-10, 2026): 27b428e5, 2526b88c, d9c75c43, 8e89290f

AGENT ARCHITECTURE: Agent roles naturally stratify into orchestrator (Chief), creator (Blog Writer), reviewer (Content Reviewer), automator (Demo Prep) — mirroring organizational hierarchy. Permission levels (agent_full, agent_analyst, agent_readonly) map cleanly to org roles. AI Operations Stack pattern emerged organically from operational needs, not top-down design.

TRIPLE WIN: Every agent deployed serves three simultaneous purposes: operational leverage (time saved), product validation (dogfooding agent registry), and narrative ammunition (investor/customer proof points). Prioritize agents maximizing all three.

WORKSPACE HIERARCHY REQUIREMENT: Flat workspace structure breaks the VC and advisory firm value propositions. VCs need their own strategy PLUS cross-portfolio visibility ("which portfolio companies have highest strategic drift?"). Advisory firms need their own workspace PLUS client workspace visibility. Required: parent/child workspace hierarchy with cross-workspace querying and role-appropriate access. Without this, each workspace is an island.

MULTI-WORKSPACE API ACCESS: MCP API keys are scoped to single workspaces, blocking fluid movement between Stratafy and customer workspaces. Critical blocker for scaling customer onboarding and the advisory firm use case. Required: API keys accessing multiple workspaces with select_workspace toggling between them.

## Classification
- **Source**: stratafy chat
- **Category**: product
- **Impact**: high
- **Confidence**: likely
- **Status**: processed
- **Actionable**: Yes
- **Tags**: synthesized, agent-architecture, workspace-hierarchy, multi-workspace, api-access, vc-channel, advisory-channel, platform-gaps


