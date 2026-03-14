---
id: 8516fb8a-3fbd-4e78-9e21-ceb6790e1101
type: strategy
status: active
strategyType: product
parent: 0a24cfc9-4e6d-48dc-9a0b-9f4f951a4222
---

# Strategic AI Infrastructure

## Description
Build the opinionated, strategy-native infrastructure layer that makes Stratafy's context engineering fundamentally superior to generic AI agent memory/context plays. Seven capabilities across three phases, each with measurable objectives.

## Content
# Strategic AI Infrastructure

## The Strategic Choice

The AI agent memory/context market is building horizontal infrastructure — storage, retrieval, ingestion — that works for any domain. $45M+ has been funded in this space in 18 months (Mem0 $24M, Letta $10M, HydraDB $6.5M, Zep $2.3M). Stratafy's bet is that *strategy is too structured, too relational, and too consequential* for generic infrastructure.

Every capability the generic plays offer, Stratafy must offer an opinionated, strategy-native equivalent that is fundamentally better for strategic decisions.

This isn't about competing with these players. It's about ensuring Stratafy's infrastructure layer is as defensible as its strategic schema — so that even if someone builds a "strategy app" on top of generic context infrastructure, they can't match the depth of a system where the infrastructure itself understands strategy.

## The Seven Capabilities

Each maps to what the generic plays have, but with an opinionated strategic interpretation:

### 1. Strategic Schema (✅ Built)
**Generic:** Vector embeddings + graph overlays
**Stratafy:** Typed entities (strategies, initiatives, objectives, metrics, assumptions, risks, signals, insights, decisions) with relational links, alignment scores, health checks, and entity-level intelligence. The schema IS the opinion.

### 2. Strategy-Aware Retrieval (🟡 Partial)
**Generic:** Cosine similarity, some with hybrid BM25
**Stratafy:** Unified search across all entity types ranked by *strategic relevance*, not similarity. BM25 (keyword) + pgvector (semantic) + MCP structured queries, with ranking that understands strategic context: role, current initiative, decision type. When a CEO asks "what should I worry about?", the system retrieves high-impact risks, failing metrics, and unvalidated assumptions — not the 10 nearest vectors.

### 3. Strategic Extraction & Ingestion (🟡 Partial)
**Generic:** Chunking pipelines, sliding window enrichment
**Stratafy:** Two modes:
- **Capture pipeline** (built): URL → extract → strategic digest + signal + insight + strategy links
- **Bulk enterprise ingestion** (gap): Upload board deck/OKR sheet → extract strategy tree in 10 minutes. Critical for enterprise onboarding — without it, adoption friction is too high for companies with existing strategic artifacts.

### 4. Strategic Evolution / Time-Travel (🔴 Gap)
**Generic:** Temporal graphs (HydraDB), append-only ledgers
**Stratafy:** Temporal strategy graph showing how strategy evolved over time. Snapshot the entire strategy tree at any point. "Strategy diff" between periods. "When did we add this initiative?" "What assumption changed that caused this pivot?" This is the biggest infrastructure gap and potentially the strongest differentiator — no generic play can answer "how has our strategy evolved?" because they don't know what strategy is.

### 5. Workspace as State (🟡 Partial)
**Generic:** Cross-session memory, preference accumulation
**Stratafy:** The workspace IS persistent strategic state — inherently superior to bolted-on memory. Every MCP call reads from and writes to the same strategic architecture. Gap: interaction pattern intelligence. Who queries what, when? Strategic engagement analytics feeding Pulse drift detection. Not "memory" — *strategic attention signals*.

### 6. Hot Strategic Context (🔴 Gap)
**Generic:** In-memory processing, sub-200ms
**Stratafy:** Pre-computed, cached strategic context for <100ms AI response times. The most frequent queries (workspace snapshot, strategy tree, current priorities) should be materialized views / cache so that when a user starts a conversation, the agent has full strategic context instantly. Critical for the "strategy available wherever decisions happen" vision.

### 7. Role-Aware Access & Audit (🟡 Partial)
**Generic:** Multi-tenancy, RBAC, SOC2/GDPR
**Stratafy:** Multi-tenancy exists (workspaces). Gap: role-aware views (board member sees full tree at summary level; product manager sees their initiative context; investor sees pitch view) and decision audit trails (who decided what, based on what intelligence). Enterprise requirement.

## Why This Is Defensible

1. **The schema is the moat.** Stratafy's data model encodes strategic architecture — strategies with typed children, assumptions linked to contexts, signals routed to strategies with impact scores. You can't build this on top of a flat embedding store.

2. **Retrieval knows what "relevant" means.** In a strategic context, relevance is defined by role, initiative ownership, risk exposure, and assumption dependency — not vector distance.

3. **Ingestion extracts structure, not chunks.** A board deck becomes a strategy tree. A competitor announcement becomes a signal linked to affected strategies. Generic ingestion produces chunks; Stratafy produces strategic architecture.

4. **Versioning tracks strategic evolution, not data changes.** "How has our strategy evolved?" is a fundamentally different question from "what changed in the database?"

## Phasing

**Phase 1 (Q2 2026):** Hybrid retrieval, bulk ingestion, hot context cache — the capabilities that directly unblock enterprise onboarding and AI interaction quality.

**Phase 2 (Q3 2026):** Strategic time-travel, engagement analytics — the capabilities that create compounding value and board-level differentiation.

**Phase 3 (Q3-Q4 2026):** Role-aware access and audit trails — the capabilities that unlock enterprise pricing tiers and compliance requirements.

## Strategic Constraints

- Build only what the next customer needs — avoid over-engineering before PMF
- Every capability must be opinionated (strategy-specific), not generic
- Infrastructure must serve both the Strategy Workbench AND the Strategic Layer (MCP/agent access)
- Do not replicate what Supabase/PostgreSQL already provides well — extend it with strategic semantics

## Key Initiatives
- [Role-Aware Access & Audit Trails](../initiatives/role-aware-access-audit-trails.md)
- [Strategic Engagement Analytics](../initiatives/strategic-engagement-analytics.md)
- [Hot Strategic Context Cache](../initiatives/hot-strategic-context-cache.md)
- [Strategic Evolution & Time-Travel](../initiatives/strategic-evolution-time-travel.md)
- [Bulk Strategic Ingestion](../initiatives/bulk-strategic-ingestion.md)
- [Hybrid Strategic Retrieval](../initiatives/hybrid-strategic-retrieval.md)

## Alignment Score
Not calculated

## Time Horizon
medium_term
