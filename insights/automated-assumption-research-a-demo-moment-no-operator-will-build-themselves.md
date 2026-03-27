---
id: c84bf842-4be9-4c4b-a65e-f6f3433cc03e
type: insight
source: execution_session
category: product
impactLevel: high
confidenceLevel: likely
status: pending
actionable: true
---

# Automated Assumption Research — A Demo Moment No Operator Will Build Themselves

## Summary
Stratafy's automated assumption research — generating queries, fetching web content, logging structured evidence with direction — is a feature no operator will build in Notion. It converts weeks of manual market research into seconds of automated validation, with a structured evidence trail that feeds directly into strategy reviews.

## Description
**The observation:** Stratafy already has a `research_assumption` tool that takes any assumption, generates intelligent search queries, fetches and synthesises web content, and logs structured evidence automatically. This is not a feature most people know exists — and it's one that no reasonable operator would build themselves in Notion.

**Why this is more valuable than it looks:**

Traditional strategy work involves assumptions that sit untested for months or years. A company writes "financial institutions are willing to pay R1-3M for an 18-month change management project" as an assumption, and nobody validates it until a prospect laughs at the number. Stratafy can run external research against that assumption automatically — pulling analyst reports, pricing benchmarks, case studies, competitor data — and log structured evidence that either supports, contradicts, or nuances the assumption. This happens in seconds, not weeks.

The value compounds across three dimensions:

1. **Speed of validation** — what used to require a consultant doing market research for two weeks can be surfaced in a single session. Not perfect research, but directionally useful evidence that raises or lowers confidence in a structured, trackable way.

2. **Continuous monitoring** — assumptions don't just need to be validated once; they decay over time as markets shift. An assumption that was "likely" in Q1 2025 might be "hypothesis" again by Q4 2025 if market conditions changed. Automated research can be scheduled or triggered by signals to continuously re-test assumptions against current external data.

3. **The evidence trail as a product** — the accumulation of evidence against assumptions over time is itself a valuable artefact. When a client presents to their board, they can show not just their strategy but the evidence trail that underpins their assumptions. "We believe X, and here's why — here's the external research, the customer conversation, the market signal that together justify this confidence level." That's a board-level feature that no document system produces.

**The current limitation and how to fix it:**

The `research_assumption` tool as it exists today uses the assumption name as the search query — which is why the automated research earlier today returned junk (Google returned bot-detection pages for overly specific queries like "Prospects feel document model pain acutely enough to motivate adoption 2026"). The fix is to make the tool smarter about query generation: decompose the assumption into 2-3 targeted sub-questions, use shorter and more precise search queries, and layer web search with content fetching for depth.

Once the query generation is good, the feature becomes genuinely magical — you log an assumption, click research, and within a minute you have structured external evidence logged against it with direction, sources, and a confidence update recommendation.

**The Notion comparison:**

There is no version of this in Notion. An operator could theoretically set up a Notion agent that searches the web and writes findings to a database — but it would have no concept of assumption confidence levels, no structured direction (supports/contradicts/neutral), no link to strategic entities, no evidence trail that feeds into strategy reviews. They'd be building a research filing system, not a validation engine.

**Product priority implication:**

This feature should be prominently demonstrated in every sales session. The sequence that creates maximum impact: (1) show an assumption in the client's workspace, (2) click research, (3) watch real external evidence populate against it in real time. The "wait, how does it do that?" moment is available right now — it just needs the query generation to be reliable enough that it doesn't fall flat.

## Classification
- **Source**: execution session
- **Category**: product
- **Impact**: high
- **Confidence**: likely
- **Status**: pending
- **Actionable**: Yes
- **Tags**: product-strategy, assumption-research, demo-moment, differentiation, automation, notion-comparison


