---
id: b8fd7610-b119-48e3-a11b-5c9001c75f95
type: insight
source: stratafy_chat
category: strategic
impactLevel: high
confidenceLevel: confirmed
status: synthesized
actionable: true
---

# Manual-first feature development creates built-in case studies

## Summary
Every Stratafy feature follows an emergent pattern: do it manually with AI + human triage, document what works, then build the automated version. This means every feature ships with a pre-existing case study. Perspective Reviews already have STR-119/STR-120 as evidence before a line of product code is written.

## Description
This session itself was a Perspective Review. We took an external AI output (Grok reviews), applied structured triage (accept/defer/dismiss with rationale), routed accepted findings into the strategy infrastructure (insights, Linear issues), and captured the meta-learning as new insights.

This is the third consecutive session where the work Stratafy is doing IS the work Stratafy sells. Previous examples: using Stratafy to manage Stratafy's own strategy (dogfooding), using the radar to scan the AI landscape and route findings into assumptions. Now: using an external review process to design the internal review feature.

The pattern is becoming a proof architecture:
1. Do the work manually using AI + human triage
2. Document what worked and what didn't
3. Design the product feature based on the manual process
4. Build the automated version
5. Show the before/after

This means every feature Stratafy builds has a built-in case study from the manual version. Perspective Reviews already have STR-119 (good) and STR-120 (bad) as documented evidence. The product feature (STR-121) codifies the process.

Implication for ScaleUp demo (Feb 23): Don't just show the product. Show the manual version first ("here's what happens when you ask AI for a CFO review without context"), then show what Stratafy does with context. The contrast IS the demo.

Implication for Sequoia pitch: The methodology content isn't just marketing — it's the R&D log. Every methodology article describes a process we've tested manually before building into software. This is unusually rigorous for a pre-seed company and should be highlighted.

## Classification
- **Source**: stratafy chat
- **Category**: strategic
- **Impact**: high
- **Confidence**: confirmed
- **Status**: synthesized
- **Actionable**: Yes
- **Tags**: methodology, case-study, dogfooding, development-process, demo-strategy


