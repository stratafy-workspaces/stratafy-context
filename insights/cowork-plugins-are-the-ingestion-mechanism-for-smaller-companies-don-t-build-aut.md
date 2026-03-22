---
id: eef589f2-b913-4df6-b5aa-705659c3413a
type: insight
source: execution_session
category: product
impactLevel: high
confidenceLevel: confirmed
status: pending
actionable: true
---

# Cowork plugins ARE the ingestion mechanism for smaller companies — don't build automated pipelines prematurely

## Summary
Claude Cowork plugins (strategy-first-principles, strategic capture, workspace builder) provide guided, schema-aware workspace creation that is the right ingestion approach for current smaller customer segment. The evolution path is: plugins today → semi-automated extraction → full bulk pipeline when enterprise demands it.

## Description
The original Bulk Strategic Ingestion initiative assumed enterprise customers needing automated PDF→strategy tree pipelines. But the current customer segment is smaller companies where the Cowork plugins are a better fit:

1. **Plugins understand the schema natively** — they guide users through creating proper strategic architecture using Stratafy's first-principles framework, not just chunking documents into flat entities
2. **Human-in-the-loop is a feature, not a limitation** — for strategy (which is high-stakes and requires judgment), guided creation is better than automated extraction with 85% accuracy
3. **Plugins are already built and working** — no additional engineering investment needed
4. **The evolution path is natural**: plugins → plugin-assisted extraction (plugin reads a PDF and proposes entities via MCP) → fully automated pipeline. Each step builds on the previous one and is triggered by actual customer demand

This insight resolves the tension between the over-engineering risk and the ingestion gap. The gap isn't actually a gap for the current segment — it's addressed by a different mechanism than originally planned.

Strategic implication: invest in making the Cowork plugins better (more skills, better coaching prompts, faster workspace setup) rather than building automated ingestion infrastructure that no current customer needs.

## Classification
- **Source**: execution session
- **Category**: product
- **Impact**: high
- **Confidence**: confirmed
- **Status**: pending
- **Actionable**: Yes
- **Tags**: ingestion, plugins, cowork, phasing, smaller-companies, pmf


