---
id: b2a16530-c8d2-4fad-9099-adf120e8dbec
type: initiative
status: in_progress
priority: critical
strategy: Strategic AI Infrastructure
completionPercentage: 65
---

# Universal Entity Embedding & Semantic Search

## Description
Extend pgvector embeddings from documents to all strategy entity types — strategies, initiatives, objectives, decisions, assumptions, risks, insights, metrics, beliefs, values, principles. Single entity_embeddings table with type discriminator. One embedding per entity. Unified search_workspace MCP tool for cross-entity semantic search. Background generation on create/update plus backfill for existing entities. Phases: (1) high-value entities + unified search, (2) remaining types, (3) agent context injection, (4) cross-entity relationship discovery. Foundational for AI context injection and "show me everything about X" queries.

## Parent Strategy
[Strategic AI Infrastructure](../strategy/product/strategic-ai-infrastructure.md)

## Status & Progress
- **Status**: in progress
- **Priority**: critical
- **Completion**: 65%

## Key Objectives
No objectives defined

## Timeline
- **Start Date**: 2026-02-25
- **Target Date**: 2026-04-15

## Content
## Implementation Status

### Phase 1: High-Value Entities + Unified Search — COMPLETE
- **Entity Embedding Service** (`layers/ai/server/services/entity-embedding-service.ts`): Config-driven embedding for 11 entity types (strategy, initiative, plan, decision, assumption, risk, insight, metric, objective, signal, key_priority) using Voyage AI. Content-hash deduplication, batch processing with 5-concurrent limit, 5-min debounce.
- **Workspace Search Service** (`layers/ai/server/services/workspace-search-service.ts`): Unified semantic search across 12 types (11 entities + documents). Enrichment layer with batch-fetched entity details, archived/inactive filtering, similarity scoring with metadata.
- **Cron Integration** (`server/api/_cron/distillation.get.ts`): `processAllPendingEntityEmbeddings` runs every cron cycle. Polls for entities where `embedded_at < updated_at`.
- **Database**: `embedded_at` column on all entity tables, `ai_embeddings` table with `content_type` discriminator, `ai_match_embeddings_text` RPC for vector similarity.
- **REST API** (`layers/ai/server/api/ws/[id]/ai/workspace-search.post.ts`): Zod-validated endpoint with entity type filtering, threshold & limit controls.
- **MCP Tool**: `search_workspace` registered in MCP server for cross-entity semantic search.
- **Frontend**: `WorkspaceSearch.vue` component with entity type filtering and workspace-scoped search UI.

### Phase 2: Remaining Entity Types — COMPLETE
All entity types from the original scope are covered. Implementation exceeds original scope by also including plan, signal, and key_priority.

### Phase 3: Agent Context Injection — NOT STARTED
No automatic injection of embedding results into agent/bot context. The `search_workspace` MCP tool allows manual queries, but agents don't yet auto-pull relevant embeddings before responding.

### Phase 4: Cross-Entity Relationship Discovery — NOT STARTED
No relationship discovery logic based on embedding similarity. The infrastructure exists (shared embedding space), but no automated "this risk relates to that decision" discovery has been built.
