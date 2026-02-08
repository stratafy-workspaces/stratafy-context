---
id: 5792667f-ef41-42cb-a41c-5956f7071df8
type: insight
source: stratafy_chat
category: technology
impactLevel: critical
confidenceLevel: confirmed
status: processed
actionable: true
lastUpdated: 2026-02-06T13:28:17.615021+00:00
---

# Strategic Context Distribution Architecture: Pre-computed, Role-Scoped, Regenerated on Change

## Summary
Strategic context for agents and humans should be generated via role-specific prompts, stored as snapshots, and regenerated whenever the underlying strategy changes—not computed on-the-fly.

## Description
Core architectural insight from discussion with Ignatius about technical co-founder role:

**The Problem:**
AI agents and humans at different organizational levels need strategic context, but they need different scopes and summaries. Giving everyone the full strategy creates noise and potential security/permission issues. Computing context on-demand is slow and inconsistent.

**The Solution Architecture:**

1. **Role/Agent-Specific Prompts:** Each consumer type (CEO, board, manager, IC, investor, prospect, sales agent, support agent, planning agent) has a dedicated summarization prompt that extracts relevant strategic context from the full strategy.

2. **Generate and Store Snapshots:** Running the prompt produces a context package that gets stored—not generated on every request.

3. **Regenerate on Strategy Change:** When underlying strategy updates, all context snapshots are regenerated automatically. Stored versions always reflect current strategy state.

4. **Serve from Storage:** Agents and humans pull pre-computed context—fast, consistent, version-controlled.

**Why This Matters:**
- Performance: No waiting for summarization at access time
- Consistency: Same role = same context at any given moment
- Auditability: Track what context was available at any point in time
- Cost efficiency: Summarization runs on strategy change, not every request
- Synchronization: Drift eliminated by design—regeneration is triggered by source changes

**The Principle:** Strategic context is a derived artifact that stays synchronized through regeneration, not real-time computation.

This extends Role-Aware Strategic Intelligence to include AI agents as first-class consumers, and establishes the mechanical pattern for how Stratafy distributes strategy to any consumer—human or AI, internal or external.

## Classification
- **Source**: stratafy chat
- **Category**: technology
- **Impact**: critical
- **Confidence**: confirmed
- **Status**: processed
- **Actionable**: Yes
- **Tags**: architecture, role-aware, agents, context-distribution, permissions, ignatius-discussion, technical-foundation


