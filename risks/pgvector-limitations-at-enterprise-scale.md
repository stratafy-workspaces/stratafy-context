---
id: d38fc939-eff2-4501-bc88-b5c4bf0adf5c
type: risk
riskType: technical
riskSource: internal
likelihood: low
impact: high
riskScore: 3
status: active
mitigationStatus: identified
---

# pgvector limitations at enterprise scale

## Description
Current semantic search relies on pgvector within Supabase PostgreSQL. Enterprise workspaces with thousands of strategies, documents, signals, and insights may hit performance or accuracy limitations. pgvector's HNSW index works well at moderate scale but may degrade for large workspaces with complex cross-entity queries. HydraDB's entire thesis is that vector databases break at scale — if true for pgvector, Stratafy's retrieval infrastructure needs architectural evolution (e.g., dedicated vector service, hybrid architecture, or the structured MCP approach may actually outperform embeddings for strategic queries).

## Assessment
- **Likelihood**: low
- **Impact**: high
- **Risk Score**: 3
- **Type**: technical
- **Source**: internal
- **Status**: active

## Mitigation
- **Status**: identified
- **Plan**: Monitor pgvector query performance as workspaces grow. Set threshold: if p95 vector search latency exceeds 500ms for a workspace, evaluate alternatives. The hybrid retrieval initiative (BM25 + vector + structured) naturally reduces dependency on vector search alone — structured MCP queries may handle the majority of strategic retrieval needs.
- **Review Date**: Not scheduled

