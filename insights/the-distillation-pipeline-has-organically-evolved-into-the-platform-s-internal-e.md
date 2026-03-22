---
id: 31871999-917d-41a9-a5fd-eda175e85887
type: insight
source: architecture_review
category: technology
impactLevel: high
confidenceLevel: confirmed
status: pending
actionable: true
---

# The distillation pipeline has organically evolved into the platform's internal event bus — formalise this

## Summary
What started as entity summarisation now handles summarisation, embedding, health scoring, and content quality across all entity types. Every layer plugs into it. Formalising it as an event-driven bus (with event types, subscriber registration, error isolation) would make feedback loop closure architecturally clean rather than ad-hoc.

## Description
## Maps To
- **Strategic AI Infrastructure** — core infrastructure pattern
- **Strategic Intelligence** → multiple initiatives that depend on distillation outputs
- **Strategic AI Infrastructure** → Strategic Engagement Analytics (proactive alerts would subscribe to distillation events)

## Evolution Traced Through Dev Reports
- Week 2: Summarisation adapter for strategies
- Week 4: Expanded to initiatives, plans, decisions, assumptions, risks, metrics
- Week 5: Document summarisation, PostgREST fix unblocking 727 entities, parallel processing
- Week 7: Health scoring added as post-distillation step
- Week 8: Content quality scoring extended to 6 entity types

## Recommendation
Formalise with: (1) explicit event types (entity_updated, distillation_complete, health_score_changed), (2) subscriber registration so new features hook in without modifying the pipeline, (3) error isolation so a failing subscriber doesn't block others. The "proactive alerts" objective becomes a natural subscriber rather than a separate system.

## Why This Matters
The feedback loop closure is architecturally cleanest through the distillation pipeline. "Health score dropped" → emit event → alert subscriber → surfaces in coaching prompt context.

## Classification
- **Source**: architecture review
- **Category**: technology
- **Impact**: high
- **Confidence**: confirmed
- **Status**: pending
- **Actionable**: Yes
- **Tags**: distillation-pipeline, event-bus, architecture-pattern, infrastructure


