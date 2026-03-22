---
id: 3d804525-e53b-4047-a078-ee67275e0f8e
type: decision
decisionType: type_1_irreversible
status: decided
decidedAt: 2026-03-15T10:26:29.693+00:00
---

# Architectural boundary: Strategic AI Infrastructure owns retrieval/assembly/delivery; Role-Aware Strategic Intelligence owns persona logic and UX surfaces

## Description
An overlap analysis between Strategic AI Infrastructure and Role-Aware Strategic Intelligence identified three areas of dangerous ambiguity: (1) Context Intelligence v2 and Hybrid Strategic Retrieval were describing the same retrieval/assembly mechanism from different angles; (2) Agent Registry & Context Packaging and Strategic Ingestion & Provenance Pipeline shared the same data substrate with an undocumented dependency; (3) Context Intelligence v2 and MCP Server Optimisation were both solving context window bloat from different sides with no coordination link. A clear ownership boundary was needed before any team expansion.

## Details
- **Type**: Type 1 (Irreversible)
- **Status**: decided
- **Authority**: Leonard Cremer (Founder & CEO)
- **Deadline**: No deadline
- **Decided At**: 2026-03-15T10:26:29.693+00:00

## Context
No context recorded

## Research
Cross-analysis of 7 initiatives under Strategic AI Infrastructure and 5 under Role-Aware Strategic Intelligence on 15 March 2026. Three overlaps identified: (1) Context Intelligence v2 vs Hybrid Strategic Retrieval — same capability, different framing; (2) Agent Registry vs Provenance Pipeline — shared data substrate, undocumented dependency; (3) Context Intelligence v2 vs MCP Server Optimisation — same context bloat problem, different angles.

## Decision
Strategic AI Infrastructure owns the full context stack — retrieval, assembly, caching, delivery, and MCP server optimisation. All other strategies, including Role-Aware Strategic Intelligence, are consumers of this layer, not builders of their own context mechanisms. Context Intelligence v2 is a specification for how the infrastructure layer should serve role-aware queries, not a separate implementation.

## Rationale
Without this boundary, the retrieval and context assembly layer risks being built twice as the team scales. Setting this now prevents ambiguity in investor conversations and future engineering handoffs. It also resolves the overlap between MCP Server Optimisation and Context Intelligence v2 by positioning them as coordinated infrastructure concerns under a single owner.

## Outcome
No outcome recorded yet
