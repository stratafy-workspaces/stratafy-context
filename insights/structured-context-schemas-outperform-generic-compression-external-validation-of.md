---
id: 100e8f6b-c3c7-420d-8a63-80d6833f7dc8
type: insight
source: manual
category: technology
impactLevel: high
confidenceLevel: confirmed
status: pending
actionable: true
---

# Structured context schemas outperform generic compression — external validation of Stratafy's typed entity approach

## Summary
Factory.ai's research across 36,611 production messages proves that structured, section-based context management (3.70/5) significantly outperforms freeform compression from OpenAI (3.35) and Anthropic (3.44). Their "anchored iterative" approach — merging into persistent structured state rather than regenerating — directly validates Stratafy's typed entity schema and provenance pipeline architecture.

## Description
Factory.ai published research (Dec 2025) comparing three context compression approaches for long-running AI agent sessions. Key findings with direct Stratafy relevance:

1. **Structure forces preservation.** Dedicated sections for different information types prevent silent information loss — the summarizer must populate each section or explicitly leave it empty. This is the same principle behind Stratafy's typed entity schema (strategies, initiatives, assumptions, risks, decisions).

2. **Artifact tracking needs dedicated infrastructure.** All methods scored poorly (2.19–2.45/5) on knowing which entities changed. Factory concludes this requires "a separate artifact index" beyond summarization. Stratafy's provenance pipeline (95% complete) is exactly this — validating it as architecturally necessary, not optional.

3. **Tokens per task > tokens per request.** Aggressive compression that causes re-fetching costs more overall. Directly informs the Hot Context Cache initiative — context_token_counts levels should optimise for task completion, not payload minimisation.

4. **Incremental merging beats regeneration.** Anthropic regenerates full summaries and loses details across cycles. Factory merges incrementally into persistent state. Stratafy's workspace snapshot currently regenerates per call — incremental updates would improve multi-turn plugin session fidelity.

5. **Evaluation gap.** Factory's 4-probe framework (recall, artifact, continuation, decision) could be adapted as a quality gate for Stratafy's context delivery to plugins.

Competitive context: Factory, OpenAI, and Anthropic are all investing heavily in context management for coding agents. Nobody is building strategy-domain-specific context infrastructure — Stratafy's position is unique and now externally validated.

## Classification
- **Source**: manual
- **Category**: technology
- **Impact**: high
- **Confidence**: confirmed
- **Status**: pending
- **Actionable**: Yes
- **Tags**: context-engineering, ai-infrastructure, competitive-intelligence, evaluation-methodology, provenance


