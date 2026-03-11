---
id: 0b0111b1-6b21-473f-9f00-001494ebfee6
type: insight
source: reflection
category: product
impactLevel: critical
confidenceLevel: hypothesis
status: synthesized
actionable: true
---

# Role-adaptive agent prompt is the highest-risk architectural bet

## Summary
Role-adaptive agent prompts are high-risk: success means personalized AI, failure means users revert to ChatGPT.

## Description
The system that generates context-aware prompts for AI agents based on workspace role, active strategy, and user permissions is the most technically ambitious component. If it works, every AI interaction feels personalized and strategically coherent. If it fails, the AI feels generic and users revert to ChatGPT. The risk is that context windows are finite and we're trying to stuff too much strategic context into each prompt. We need aggressive pruning heuristics and a clear hierarchy of what context matters most.

## Classification
- **Source**: reflection
- **Category**: product
- **Impact**: critical
- **Confidence**: hypothesis
- **Status**: synthesized
- **Actionable**: Yes
- **Tags**: ai-agents, context-generation, architecture, risk


