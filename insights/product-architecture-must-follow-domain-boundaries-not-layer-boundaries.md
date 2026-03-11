---
id: 5ee77f25-6a98-4e0d-b472-1672233a515f
type: insight
source: reflection
category: product
impactLevel: high
confidenceLevel: likely
status: pending
actionable: true
---

# Product Architecture Must Follow Domain Boundaries, Not Layer Boundaries

## Summary
Both the InsightSync/Pulse distinction and plugin packaging strategy point to the same principle: domain-scoped boundaries create cleaner architecture AND better GTM units than layer-scoped boundaries.

## Description
Two insights, from different contexts, converge on an architectural principle that should govern product strategy organization. InsightSync (synchronous, session-based) and Pulse (asynchronous, recurring) must remain architecturally distinct because they serve fundamentally different interaction patterns — conflating them breaks both. Similarly, domain-per-plugin (HR plugin, finance plugin) creates natural purchasing units mapped to buyer roles, while layer-per-plugin (data plugin, reporting plugin) fragments the value prop. The implication for Product Architecture: the current strategy tree organizes sub-strategies partly by layer (Strategic Intelligence, Role-Aware Intelligence) and partly by domain (Partner Plugin Ecosystem). These insights suggest leaning harder into domain boundaries. This also affects how the Partner Ecosystem Channel is structured — partners think in domains (HR, finance, operations), not in product layers.

Synthesized from: InsightSync vs Pulse architectural distinction, domain-per-plugin GTM model.

## Classification
- **Source**: reflection
- **Category**: product
- **Impact**: high
- **Confidence**: likely
- **Status**: pending
- **Actionable**: Yes
- **Tags**: synthesis, product-architecture, domain-boundaries, plugin-ecosystem


