---
id: 8516fb8a-3fbd-4e78-9e21-ceb6790e1101
type: strategy
status: active
strategyType: product
parent: 0a24cfc9-4e6d-48dc-9a0b-9f4f951a4222
---

# Strategic AI Infrastructure

## Description
Building AI-native strategic infrastructure for autonomous strategy management

## Content
# Strategic AI Infrastructure

## The Strategic Choice

The AI agent memory/context market is building horizontal infrastructure — storage, retrieval, ingestion — that works for any domain. $45M+ has been funded in this space in 18 months (Mem0 $24M, Letta $10M, HydraDB $6.5M, Zep $2.3M). Stratafy's bet is that *strategy is too structured, too relational, and too consequential* for generic infrastructure.

Every capability the generic plays offer, Stratafy must offer an opinionated, strategy-native equivalent that is fundamentally better for strategic decisions.

This isn't about competing with these players. It's about ensuring Stratafy's infrastructure layer is as defensible as its strategic schema — so that even if someone builds a \"strategy app\" on top of generic context infrastructure, they can't match the depth of a system where the infrastructure itself understands strategy.

## The Seven Capabilities

Each maps to what the generic plays have, but with an opinionated strategic interpretation:

### 1. Strategic Schema (✅ Built)
**Generic:** Vector embeddings + graph overlays
**Stratafy:** Typed entities (strategies, initiatives, objectives, metrics, assumptions, risks, signals, insights, decisions) with relational links, alignment scores, health checks, and entity-level intelligence. The schema IS the opinion.

### 2. Strategy-Aware Retrieval (🟡 Partial → Active)
**Generic:** Cosine similarity, some with hybrid BM25
**Stratafy:** Unified search across all entity types ranked by *strategic relevance*, not similarity. BM25 (keyword) + pgvector (semantic) + MCP structured queries, with ranking that understands strategic context: role, current initiative, decision type.

### 3. Strategic Ingestion & Provenance (✅ Built)
**Generic:** Chunking pipelines, sliding window enrichment
**Stratafy:** A provenance-aware mutation pipeline built into the MCP middleware layer. Every mutation across 11 executive plugins is tracked with full causal chain: source plugin → command → reasoning → entity change. Four provenance fields (`_source_plugin`, `_source_command`, `_source_ref`, `_change_reasoning`) injected into every tool schema. ~80 mutation tools tracked; lightweight writes excluded.

**What's live:**
- Fire-and-forget provenance logging on every mutation (provenance_records table)
- Server-computed enhanced fields: change_magnitude, evidence_type, confidence_score
- LLM reason and intent captured from every tool call
- Provenance UI at /provenance with entity name resolution, user attribution, filters, tooltips
- All 11 plugin prompts updated with provenance instructions (22 files, 12 mutation commands)
- Daily snapshot versions enriched with provenance_summary and LLM-assessed ai_assessment (magnitude/confidence/narrative/coherence)
- 168+ unit tests covering the full pipeline

**Deferred:** Role-based governance gates (Phase 2) — owners auto-commit today, members will create proposals when team workspaces need it. Bulk ingestion sits on top of the same middleware when enterprise scale demands it.

### 4. Strategic Evolution / Time-Travel (✅ Built — 97%)
**Generic:** Temporal graphs (HydraDB), append-only ledgers
**Stratafy:** Temporal strategy graph with daily snapshots, version-referenced architecture (content stripped, replaced with version_id refs), field-level changelog, content diffs, foundation diffing, git commit cross-referencing, AI narrative summaries (grok-3-mini-fast-beta, lazy cached), and causal chain detection across typed strategic relationships. Now enriched with provenance: each auto-version carries a provenance_summary (which plugins, commands, actors, reasoning) and an LLM ai_assessment (magnitude, confidence, narrative, coherence). Remaining: board reporting template and consumption-layer polish.

### 5. Workspace as State (🟡 Partial)
**Generic:** Cross-session memory, preference accumulation
**Stratafy:** The workspace IS persistent strategic state — inherently superior to bolted-on memory. Every MCP call reads from and writes to the same strategic architecture. Gap: interaction pattern intelligence (deferred — needs active workspaces first).

### 6. Hot Strategic Context (🔴 Gap → Active)
**Generic:** In-memory processing, sub-200ms
**Stratafy:** Pre-computed, cached strategic context for <100ms AI response times. The most frequent queries (workspace snapshot, strategy tree, current priorities) should be materialized views / cache so that when a user starts a conversation, the agent has full strategic context instantly.

### 7. Role-Aware Access & Audit (🟡 Partial → Deferred)
**Generic:** Multi-tenancy, RBAC, SOC2/GDPR
**Stratafy:** Multi-tenancy exists (workspaces). Strategy-scoped permissions deferred — current smaller customers operate with workspace-level access. Decision audit trails are now largely solved by provenance records — every strategic mutation has an accountable actor, full reasoning, plugin attribution, and LLM-assessed magnitude. Remaining: strategy-scoped read permissions and governance gates for enterprise.

## Why This Is Defensible

1. **The schema is the moat.** Stratafy's data model encodes strategic architecture — strategies with typed children, assumptions linked to contexts, signals routed to strategies with impact scores. You can't build this on top of a flat embedding store.

2. **Retrieval knows what \"relevant\" means.** In a strategic context, relevance is defined by role, initiative ownership, risk exposure, and assumption dependency — not vector distance.

3. **Every mutation has provenance.** Every workspace change traces back through a full causal chain: source content → executive plugin → command → reasoning → approval → committed change. Generic infrastructure can tell you what changed and when. Stratafy can tell you *why* — which article, which executive plugin's scan surfaced it, who approved it, and what reasoning drove the decision. This works identically whether auto-committed by an owner or reviewed by a Guardian — provenance is always captured. Each daily version carries an LLM-assessed magnitude and narrative.

4. **Versioning tracks strategic evolution, not data changes.** \"How has our strategy evolved?\" is a fundamentally different question from \"what changed in the database?\" Causal chain detection traces strategy changes back to triggering assumptions and signals — something no generic infrastructure can do without typed strategic relationships. Provenance data makes these narratives richer: every version carries the full provenance chain and an AI-generated assessment of what changed and why.

## Execution Order

The phasing follows how the work actually happens, not a theoretical sequence:

**Step 1 — Finish Time-Travel (97% done)**
Temporal query API, git cross-reference, AI change narratives, causal chain detection, provenance-enriched versioning — all live. Remaining: board reporting template, consumption-layer polish.

**Step 2 — Retrieval + Cache (next)**
Build Hybrid Strategic Retrieval and Hot Context Cache. The Provenance Pipeline is complete and capturing data. Every plugin session exercises the retrieval and context systems — pain points surface naturally.

**Step 3 — Scale when demand proves it**
Bulk Strategic Ingestion (automated pipeline through the same provenance middleware), Strategic Engagement Analytics (requires active workspaces). Activate only when customer scale demands it.

**Step 4 — Governance when enterprise requires it**
Role-Aware Access & Strategy-Scoped Permissions. Enterprise procurement blocker — build when enterprise deals are on the table. The provenance pipeline already provides decision audit trails and accountability.

## Strategic Constraints

- Build only what the next customer needs — avoid over-engineering before PMF
- Every capability must be opinionated (strategy-specific), not generic
- Infrastructure must serve both the Strategy Workbench AND the Strategic Layer (MCP/agent access)
- Do not replicate what Supabase/PostgreSQL already provides well — extend it with strategic semantics
- **Provenance at the middleware, governance by role:** Every strategic mutation carries provenance. Governance is role-based — owners auto-commit, members propose. One MCP endpoint, same tools, middleware handles everything. Plugin authors pass context, not governance logic. Zero friction for solo founders, full governance for teams.
- **Dog-food everything:** Use Stratafy's own workspace to test infrastructure capabilities as they're built

## Key Initiatives
- [Strategic Ingestion & Provenance Pipeline](../initiatives/strategic-ingestion-provenance-pipeline.md)
- [Role-Aware Access & Audit Trails](../initiatives/role-aware-access-audit-trails.md)
- [Context Consumption Analytics & Engagement Tracking](../initiatives/context-consumption-analytics-engagement-tracking.md)
- [Hot Strategic Context Cache](../initiatives/hot-strategic-context-cache.md)
- [Strategic Evolution & Time-Travel](../initiatives/strategic-evolution-time-travel.md)
- [Bulk Strategic Ingestion](../initiatives/bulk-strategic-ingestion.md)
- [Hybrid Strategic Retrieval](../initiatives/hybrid-strategic-retrieval.md)
- [MCP Server Optimisation](../initiatives/mcp-server-optimisation.md)
- [Universal Entity Embedding & Semantic Search](../initiatives/universal-entity-embedding-semantic-search.md)

## Alignment Score
Not calculated

## Time Horizon
medium_term
