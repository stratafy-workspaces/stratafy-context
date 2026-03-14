---
id: 4a83c2e1-2ead-41b7-83d2-5f1edbdd5ce8
type: insight
source: execution_session
category: product
impactLevel: high
confidenceLevel: confirmed
status: pending
actionable: true
---

# Strategic ingestion requires a two-track governance model: direct write vs. proposal pipeline

## Summary
Not all strategic changes should land directly. Trusted users/agents can write directly, but external sources, AI agents, and bulk imports need a proposal→review→approve→commit pipeline. This is the "pull request model for strategy" and shapes the entire ingestion architecture.

## Description
Strategic ingestion isn't just a technical parsing problem — it's a governance model with two distinct tracks:

**Track 1: Direct Write** — Trusted users and authorised agents who can modify strategy entities directly. Appropriate for workspace admins, strategy owners, and AI agents within tightly scoped workflows.

**Track 2: Proposal Pipeline** — Users, agents, or external sources that submit proposed changes requiring review before affecting the strategy. Applies to: bulk document imports (PDF → proposed entities), AI agent recommendations (signals proposing strategy adjustments), team member suggestions, cross-workspace inputs, and external integrations.

The proposal pipeline needs: a staging area, strategy diff view, review/approve/reject workflow, partial acceptance, and full audit trail.

Architectural implications:
1. The ingestion pipeline produces *proposals*, not *entities* — different data model required
2. Role-Aware Access must define who can direct-write vs. who must propose
3. AI agent governance becomes clearer: most agents should propose, few should direct-write
4. This is a significant differentiator — no generic AI infrastructure play has strategy-aware change governance
5. Connects ingestion, access control, and audit trails into a coherent governance architecture

## Classification
- **Source**: execution session
- **Category**: product
- **Impact**: high
- **Confidence**: confirmed
- **Status**: pending
- **Actionable**: Yes
- **Tags**: ingestion, governance, infrastructure, access-control, proposal-pipeline, ai-agents


