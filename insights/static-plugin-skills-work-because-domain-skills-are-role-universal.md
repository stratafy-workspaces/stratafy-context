---
id: 8bdee456-751d-4654-84d6-b27d0900eb29
type: insight
source: reflection
category: technology
impactLevel: high
confidenceLevel: likely
status: synthesized
actionable: true
---

# Static plugin skills work because domain skills are role-universal

## Summary
Domain skills are role-universal; only context varies per user. Static skill bundles simplify plugin development.

## Description
A strategy plugin doesn't need different skills for different users — the domain knowledge (how to run a SWOT, how to cascade OKRs, how to assess market risk) is universal. What changes per role is the context (which strategies, which metrics, which permissions), not the skills themselves. This means plugins can ship as static skill bundles while the personalization layer handles role adaptation. This dramatically simplifies plugin development and testing.

## Classification
- **Source**: reflection
- **Category**: technology
- **Impact**: high
- **Confidence**: likely
- **Status**: synthesized
- **Actionable**: Yes
- **Tags**: plugin-architecture, skills, context-generation, simplification


