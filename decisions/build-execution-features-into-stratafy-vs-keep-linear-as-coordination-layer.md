---
id: cbe44c39-7500-4aa1-8575-2cdb7f1ef2d0
type: decision
decisionType: type_1_irreversible
status: pending
---

# Build execution features into Stratafy vs keep Linear as coordination layer

## Description
Whether to build operational execution features (task management, project tracking, coordination) into Stratafy, or continue using Linear as the coordination layer in the AI Operations Stack.

This is a **Type 1 decision** — building execution features commits significant engineering resources and repositions the product from infrastructure to application.

## Core Tension

Three-tool cost per user (Claude + Stratafy + Linear) creates adoption friction, especially for channel deployments (advisory firm clients, VC portfolio companies). But building PM features diverts from the intelligence layer that differentiates Stratafy and puts us in competition with Linear, Asana, and every PM tool in a crowded market.

## Details
- **Type**: Type 1 (Irreversible)
- **Status**: pending
- **Authority**: Not specified
- **Deadline**: No deadline
- **Decided At**: Not yet decided

## Context
Pre-seed, solo founder. First paying customer (STIR) starting Feb 17. ScaleUp demo Feb 23. Sequoia pitch window April 2026. 391 commits across 31 services. Linear integration already built and operational. AI Operations Stack methodology published. No customer has yet raised the three-tool cost as a blocker.

## Research
## Arguments for Keeping Linear

1. **Core belief alignment** — "We don't compete with tools — we make them strategically intelligent" directly contradicts building PM features
2. **Infrastructure mindset over Application mindset** — task management is application thinking
3. **AI Operations Stack methodology** explicitly separates Strategic Context (Stratafy) from Coordination (Linear) — collapsing layers weakens the teachable framework
4. **Solo founder pre-seed** — 3-6 months of PM feature engineering doesn't move toward Sequoia pitch
5. **Linear free tier** covers 250 issues, sufficient for target market entry
6. **Integration stickiness** — integrating with many tools is stickier than replacing one tool

## Arguments for Building In

1. Three subscriptions per user is real friction for channel deployments
2. Simpler pitch — one platform, not a stack
3. Tighter control over the full experience
4. Revenue capture on execution layer, not just strategy layer

## Alternative Paths

1. Bundled pricing with Linear partnership
2. Stratafy-provisioned Linear workspaces
3. Lightweight task/coordination features that complement Linear rather than replace it
4. Build only after validating the friction is real with STIR and ScaleUp

## Decision
Not yet decided

## Rationale
No rationale recorded

## Outcome
No outcome recorded yet
