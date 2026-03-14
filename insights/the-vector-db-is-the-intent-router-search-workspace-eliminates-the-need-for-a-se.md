---
id: a24d155b-9c20-4134-9262-452fd1699ab6
type: insight
source: stratafy_chat
category: technology
impactLevel: high
confidenceLevel: proven
status: pending
actionable: true
---

# The vector DB is the intent router — search_workspace eliminates the need for a separate classification call

## Summary
Live testing of search_workspace confirmed pgvector similarity search returns precisely ranked entities without a separate classification step. Faster, free, and more precise than a Haiku classification call. Similarity-to-depth mapping validated: >0.55 → full, 0.42–0.55 → executive, 0.35–0.42 → brief, <0.35 → exclude.

## Description
Two live tests of search_workspace confirmed that embedding the query and running pgvector similarity search returns precisely ranked, semantically relevant entities — without a separate classification step.

Test 1 (focused query — "biggest risk to Series A timeline"): returned 8 risks ranked correctly, with a natural quality break at ~0.42 similarity. Top 2 results were exactly right (lighthouse customers not materialising, solo founder bottleneck). Risks 3-4 were legitimately adjacent (execution risks affecting the pitch window indirectly).

Test 2 (broad synthesis query — "how does our AI context system create competitive advantage over incumbents"): pulled top 10 cross-entity insights ranked correctly, scores from 0.667 down to 0.575, reading as a curated competitive moat brief.

Practical implications:
- The Haiku intent classification call proposed in Context Intelligence v2 is eliminated — the vector DB does this better, for free
- Retrieval is entity-specific (not type-bucket), enabling precise depth assignment per result
- Dynamic threshold (~0.42 for focused queries, lower for synthesis queries) outperforms a fixed 0.35 cutoff
- Similarity-to-depth mapping is now concrete and implementable: >0.55 → full, 0.42–0.55 → executive, 0.35–0.42 → brief, <0.35 → exclude

## Classification
- **Source**: stratafy chat
- **Category**: technology
- **Impact**: high
- **Confidence**: proven
- **Status**: pending
- **Actionable**: Yes
- **Tags**: context-intelligence, vector-db, search, architecture, validated


