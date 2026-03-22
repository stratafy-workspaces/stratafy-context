---
id: 5246b207-c192-49c1-8160-2ec54af9cc43
type: risk
riskType: execution
riskSource: internal
likelihood: medium
impact: high
riskScore: 6
status: active
mitigationStatus: in_progress
---

# Over-engineering infrastructure before PMF

## Description
Building enterprise-grade infrastructure (temporal graphs, caching layers, role-aware access) when the priority is lighthouse customer conversion and proving product-market fit. The original mitigation (phase strictly) failed to govern behaviour — time-travel was built before retrieval and ingestion. Corrective action taken: bulk ingestion deferred (plugins serve this today), engagement analytics and RBAC moved to draft, phasing revised to reflect actual priorities. Risk partially materialised but corrected.

## Assessment
- **Likelihood**: medium
- **Impact**: high
- **Risk Score**: 6
- **Type**: execution
- **Source**: internal
- **Status**: active

## Mitigation
- **Status**: in_progress
- **Plan**: Revised phasing now reflects reality: Phase 1 (NOW) = complete time-travel + build retrieval + build cache. Phase 2 = build only WHEN demand proves it (bulk ingestion, analytics). Phase 3 = WHEN enterprise requires it (RBAC, audit). Three initiatives moved to draft status. New constraint added: "plugins first" — invest in Cowork plugins rather than automated pipelines until customer scale demands it. Gate: do not activate Phase 2/3 initiatives until at least 3 paying customers are on the platform.
- **Review Date**: Not scheduled

