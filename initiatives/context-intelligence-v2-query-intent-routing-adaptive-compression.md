---
id: 0cae1213-f70b-47cc-b83b-52747c4bf206
type: initiative
status: draft
priority: high
strategy: Strategic Delivery
completionPercentage: 0
---

# Context Intelligence v2 — Query-Intent Routing & Adaptive Compression

## Description
Upgrade the Context Intelligence System from role-based to semantic-first, query-aware assembly. Rather than injecting maximum permitted context per role, retrieve only what the incoming query semantically requires — then intersect with the role matrix as an access ceiling. Architecture validated by live testing of search_workspace (pgvector). Delivers 50-70% token reduction on focused queries, higher signal density, and a compounding AI quality advantage that widens as workspaces mature.

## Parent Strategy
[Strategic Delivery](../strategy/product/strategic-delivery.md)

## Status & Progress
- **Status**: draft
- **Priority**: high
- **Completion**: 0%

## Key Objectives
No objectives defined

## Timeline
- **Start Date**: 2026-04-01
- **Target Date**: 2026-06-30

## Content
# Context Intelligence v2 — Query-Intent Routing & Adaptive Compression

## Problem

The current context assembly system compresses by role. The role matrix determines what each AI executive can access, but it has no awareness of what any given query actually needs. A Finance Director asking about strategic risk and the same Finance Director asking about the rebrand initiative both receive the same pre-assembled context — even though their information needs are completely different.

The result: context windows that are larger than necessary, with lower signal density, producing bounded AI output quality regardless of model capability.

## Core Architectural Shift

**From:** Maximum permitted context per role (role-based injection)
**To:** Minimum sufficient context per query, with role matrix as access ceiling

The query embeds → similarity search retrieves ranked entities → role matrix filters access → depth assigned by similarity score → system prompt assembled from minimum sufficient set.

## Validated Mechanism

Live testing of `search_workspace` (pgvector) confirmed the vector DB is the intent router. Two tests:
- Focused query ("Series A risk"): 8 risks ranked correctly, natural quality break at ~0.42 similarity
- Broad synthesis query ("AI context competitive advantage"): top 10 cross-entity insights, scores 0.667–0.575, reading as a curated competitive brief

No separate Haiku classification call needed. Faster, free, entity-specific rather than type-bucket.

**Similarity-to-depth mapping:**
- >0.55 → Full
- 0.42–0.55 → Executive
- 0.35–0.42 → Brief
- <0.35 → Exclude

---

## Phase 1 — Assembly-Time Changes (April)
*No distillation pipeline changes required*

### 1. Semantic Retrieval Replaces Role-Based Injection
Embed the incoming query, run `search_workspace`, intersect results with the role matrix. Role sets access ceiling; similarity score sets actual depth.

### 2. Dynamic Similarity Threshold
Threshold adapts to the score distribution of each query's results rather than a fixed 0.35 cutoff. Prevents noise injection on tight queries while capturing the full relevant set on broad synthesis queries.

### 3. Adaptive Query Expansion
Before searching, generate 2-3 semantic reformulations of the incoming query and run all in parallel — results merged and deduplicated. Fixes vocabulary mismatch between how users phrase questions and how entities are described in the workspace.

*Grounded in HydraDB research: single-query vector retrieval consistently misses relevant entities that differ in surface phrasing from the original query.*

### 4. Score-Based Intelligence Elevation
High-signal intelligence auto-elevates to full depth regardless of similarity score or role config:
- Risks scored >15 (likelihood × impact)
- Assumptions with confidence <0.3
- Decisions pending >14 days

Ensures critical intelligence always surfaces without manual matrix configuration.

### 5. Staleness-Weighted Depth Decay
Entity depth degrades with inactivity — one depth level down per 30-day inactivity band. Entities >90 days inactive compress to reference with a staleness flag surfaced in AI responses. Reduces token consumption for inactive workspace areas and makes data quality issues visible in conversation.

---

## Phase 2 — Distillation Pipeline Changes (May–June)
*Schema changes required*

### 6. Positional Distillation
Include parent entity `summary_short` in child entity distillation prompts. An initiative distilled without its parent strategy's framing produces a summary that cannot be retrieved on strategy-framed queries.

*HydraDB sliding window research found 40% of standard RAG chunks are semantically invisible due to unresolved implicit references when distilled in isolation. This is the Stratafy equivalent.*

### 7. Delta Context for Returning Sessions
Store `last_session_at` per user. At assembly time, prepend a change digest of entities updated since the last session, weighted by semantic relevance to recent query patterns. AI starts aware of what's new rather than cold each session.

---

## Dependency

**Universal Entity Embedding initiative (b2a16530) must cover all 11 entity types before Phase 1 ships.** Semantic retrieval with partial embedding coverage produces blind spots worse than the current role-based approach for unembedded entity types.

---

## Expected Outcomes

| Metric | Current | Target |
|---|---|---|
| Token usage (focused queries) | Role-based full set | 50-70% reduction |
| Token usage (deep workspaces) | Degrades with growth | Improves with growth |
| AI response relevance | Role-capped | Query-optimised |
| Critical intelligence surfacing | Matrix-dependent | Score-elevated always |
| Returning session quality | Cold start | Delta-aware |
