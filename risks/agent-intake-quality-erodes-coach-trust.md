---
id: 3a89cf15-5329-42a9-a653-b692ffa5c5d2
type: risk
riskType: technical
riskSource: internal
likelihood: medium
impact: critical
riskScore: 8
status: active
mitigationStatus: identified
lastUpdated: 2026-02-27T16:55:44.275891+00:00
---

# Agent Intake Quality Erodes Coach Trust

## Description
The agent intake workflow produces low-quality lead briefs — wrong industry, hallucinated challenges, poorly scaffolded workspaces — especially for early-stage companies with sparse public data. Even a few bad briefs could destroy coach trust in the platform and undermine the entire value proposition. Coaches who receive unreliable output will stop using the intake and tell peers.

## Assessment
- **Likelihood**: medium
- **Impact**: critical
- **Risk Score**: 8
- **Type**: technical
- **Source**: internal
- **Status**: active

## Mitigation
- **Status**: identified
- **Plan**: Define quality floor thresholds (auto-send vs manual review vs reject). Dogfood the agent workflow extensively before exposing to coaches. Start with manual review of every brief in Phase 1. Build confidence scoring into agent output. Implement coach feedback loop on brief quality.
- **Review Date**: Not scheduled

