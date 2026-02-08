---
id: 3ce6df99-8938-4828-bb61-06afbb082dc8
type: risk
riskType: execution
riskSource: internal
likelihood: medium
impact: high
riskScore: 6
status: active
mitigationStatus: identified
lastUpdated: 2026-02-06T21:13:20.229109+00:00
---

# Complexity creep from attempting all 7 role interfaces simultaneously

## Description
7 role interfaces (Advisor, Interface, Demo, Coach, Guide, Investor, Prospect) is ambitious. Risk of spending 2+ years building interfaces and never shipping. Each interface needs its own prompt architecture, permission model, tone calibration, and edge case handling. AI leverage makes this feasible but sequence determines success. Phased rollout is critical: Advisor (now, validated) → Demo (Q1) → Interface (Q2, post-funding) → Team interfaces (Q3-Q4). Originated from insight: Execution risk - Sequence is everything.

## Assessment
- **Likelihood**: medium
- **Impact**: high
- **Risk Score**: 6
- **Type**: execution
- **Source**: internal
- **Status**: active

## Mitigation
- **Status**: identified
- **Plan**: Enforce phased rollout sequence: Advisor → Demo → Interface → Team. Do not begin next phase until current phase is validated. Each interface ships only when the prior one has proven value. AI leverage reduces per-interface cost but does not eliminate the sequencing requirement.
- **Review Date**: Not scheduled

