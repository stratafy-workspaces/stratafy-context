---
id: 5246b207-c192-49c1-8160-2ec54af9cc43
type: risk
riskType: execution
riskSource: internal
likelihood: medium
impact: high
riskScore: 6
status: active
mitigationStatus: identified
---

# Over-engineering infrastructure before PMF

## Description
Building enterprise-grade infrastructure (temporal graphs, caching layers, role-aware access) when the priority is lighthouse customer conversion and proving product-market fit. Engineering effort diverted from customer-facing features to internal infrastructure may slow PMF timeline. The risk is spending 3 months building strategic time-travel when what the next customer actually needs is a better onboarding experience.

## Assessment
- **Likelihood**: medium
- **Impact**: high
- **Risk Score**: 6
- **Type**: execution
- **Source**: internal
- **Status**: active

## Mitigation
- **Status**: identified
- **Plan**: Phase delivery strictly: build only what the next customer needs. Phase 1 (Q2) = retrieval + ingestion + cache (directly unblock enterprise onboarding). Phase 2 (Q3) = time-travel + analytics (build only after 3+ paying customers). Phase 3 (Q4) = governance (build only when enterprise deals require it).
- **Review Date**: Not scheduled

