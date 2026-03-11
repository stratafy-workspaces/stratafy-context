---
id: 3db397a6-6d94-4a6d-99a1-68e1fd088107
type: insight
source: stratafy_chat
category: operational
impactLevel: low
confidenceLevel: confirmed
status: synthesized
actionable: false
---

# AI geographic priors override strategic context — Grok's persistent South Africa bias across both reviews

## Summary
Grok pushed Johannesburg infrastructure concerns (offline modes, load shedding, edge AI) across two separate reviews with different lenses. This reveals a geographic prior in the model that overrides actual strategic context. Relevant for designing Perspective Review lens definitions that prevent location-based pattern matching from polluting analysis.

## Description
Grok (xAI) was given Stratafy's methodology twice and asked for different perspective reviews. Both times it pushed "Johannesburg connectivity challenges," "offline modes," "load shedding resilience," and "edge/on-device AI." This persisted across a Technical Advisor lens and a Startup Advisor lens — suggesting it's a strong prior in Grok's model when South Africa is mentioned, regardless of the actual question being asked.

This is a useful signal about AI review tooling in general: AI systems have geographic priors that can override the actual strategic context. When building Perspective Reviews, the lens definitions should include explicit guidance about what the perspective should and should NOT focus on, to prevent geographic/demographic priors from polluting the analysis. The lens should interrogate what's in the workspace, not what it associates with the founder's location.

Additionally, three times Grok recommended "hire from ex-Naspers/Takealot" and "use Silicon Cape/Grindstone" — generic South African tech ecosystem references that show no awareness of the actual team strategy. This reinforces the context depth finding: without operational context, AI defaults to geographic pattern-matching.

## Classification
- **Source**: stratafy chat
- **Category**: operational
- **Impact**: low
- **Confidence**: confirmed
- **Status**: synthesized
- **Actionable**: No
- **Tags**: ai-behavior, geographic-bias, perspective-reviews, lens-design, grok


