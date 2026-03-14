---
id: a5908151-4516-481c-9f8f-7a9e2ba1072a
type: initiative
status: active
priority: high
strategy: Strategic AI Infrastructure
completionPercentage: 0
---

# Hybrid Strategic Retrieval

## Description
Build unified search across all entity types (strategies, initiatives, objectives, documents, signals, insights, decisions, assumptions, risks) combining BM25 keyword search + pgvector semantic search + structured MCP queries. Ranking must be strategy-aware: results weighted by role context, initiative ownership, risk exposure, assumption dependency — not just vector distance. When a CEO asks "what should I worry about?", the system retrieves high-impact risks, failing metrics, and unvalidated assumptions. Currently only pgvector cosine similarity is available.

## Parent Strategy
[Strategic AI Infrastructure](../strategy/product/strategic-ai-infrastructure.md)

## Status & Progress
- **Status**: active
- **Priority**: high
- **Completion**: 0%

## Key Objectives
- [60% reduction in MCP calls per complex strategic query](../objectives/60-reduction-in-mcp-calls-per-complex-strategic-query.md)
- [Cross-entity strategic queries return results within 500ms](../objectives/cross-entity-strategic-queries-return-results-within-500ms.md)

## Timeline
- **Start Date**: Not set
- **Target Date**: 2026-06-30

## Content
# Hybrid Strategic Retrieval

## The Problem

Stratafy's current retrieval is MCP tool-based: each query maps to a specific tool call (e.g., `get_strategy`, `list_initiatives`). This works for structured lookups but fails for fuzzy, cross-cutting queries like "what are the biggest risks to our growth strategy?" — which requires traversing strategies, risks, assumptions, and insights simultaneously.

Generic AI infrastructure solves this with cosine similarity over embeddings + BM25 keyword search. But flat vector search has no concept of strategic hierarchy. A risk linked to a corporate strategy should rank higher than a risk linked to a sub-initiative when answering a strategic question.

## The Approach

Build a hybrid retrieval layer that combines:

1. **Structured graph traversal** — Walk the strategy tree using entity relationships (strategy → initiative → objective, strategy → risk, etc.). This is Stratafy's native strength.
2. **Semantic search** — Vector embeddings over entity content fields, enabling fuzzy matching across the workspace.
3. **Strategic weighting** — Results ranked not just by semantic similarity but by strategic relevance: hierarchy level, link density, recency, and confidence scores.

The key insight: retrieval should be strategy-aware. A query about "market risk" should surface risks linked to GTM strategies before surfacing risks linked to operational initiatives, even if the semantic similarity scores are identical.

## Technical Design

- Embed all entity content fields (strategies, initiatives, objectives, risks, assumptions, decisions, insights) into a vector store
- Maintain a graph index of entity relationships for traversal
- Build a scoring function: `final_score = α(semantic_score) + β(graph_distance_score) + γ(hierarchy_weight) + δ(recency_score)`
- Expose as an internal API that MCP tools can call, and as a new `search_workspace` enhancement

## Success Criteria

- Cross-entity queries return relevant results within 500ms
- Strategic hierarchy weighting demonstrably improves result relevance vs. flat semantic search
- Reduces the number of MCP tool calls needed to answer complex strategic questions by 60%+

## Dependencies

- Requires entity content fields to be consistently populated (current gap in some workspaces)
- Needs embedding infrastructure (vector store selection: pgvector, Pinecone, or Qdrant)
- Builds on existing MCP tool architecture — extends rather than replaces
