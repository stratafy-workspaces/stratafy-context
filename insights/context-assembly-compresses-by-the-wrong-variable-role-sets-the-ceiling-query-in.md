---
id: dababb55-7ba8-44f9-b6d7-27acbbb80e24
type: insight
source: stratafy_chat
category: product
impactLevel: high
confidenceLevel: confirmed
status: pending
actionable: true
---

# Context assembly compresses by the wrong variable — role sets the ceiling, query intent sets the floor

## Summary
Current context assembly injects maximum permitted context per role. The right architecture injects minimum sufficient context per query, using the role matrix only as an access ceiling. These are fundamentally different compression strategies with meaningfully different output quality.

## Description
The context matrix determines what a role *can* see. It does not determine what a role *needs* for any given query. A Finance Director asking about strategic risk and the same Finance Director asking about the rebrand initiative both receive the same pre-assembled context under the current system — even though their information needs are completely different.

The correct model: embed the incoming query, retrieve semantically relevant entities, then intersect with the role matrix as a hard access ceiling. The role sets what is permitted. The query sets what is needed. Both gates must be applied; currently only one is.

This reframing changes the entire assembly architecture — from role-based pre-assembly to query-aware dynamic retrieval. The output is smaller context windows with higher signal density, which directly improves AI response quality.

## Classification
- **Source**: stratafy chat
- **Category**: product
- **Impact**: high
- **Confidence**: confirmed
- **Status**: pending
- **Actionable**: Yes
- **Tags**: context-intelligence, ai-quality, architecture


