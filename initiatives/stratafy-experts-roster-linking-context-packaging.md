---
id: f50412ff-b44c-4fc3-8eee-eb31f62db598
type: initiative
status: in_progress
priority: high
strategy: Strategic Delivery
completionPercentage: 72
---

# Stratafy Experts — Roster, Linking & Context Packaging

## Description
Define the full Stratafy Expert roster, map each AI expert to their owned strategies, and build the expert-specific context delivery path. Includes: (1) Expert roster with 11 roles seeded per workspace, (2) Strategy-to-expert linking via stratafy_expert_id FK, (3) get_expert_context(role) MCP tool that resolves expert → owned strategies → context_profiles depth/access → structured bundle, (4) Wiring context_profiles resolution chain into expert context generation. The expert path is separated from the general agent path — experts use role-based context profiles with deterministic scoping; general agents use template-based configuration via ws_agents.

## Parent Strategy
[Strategic Delivery](../strategy/product/strategic-delivery.md)

## Status & Progress
- **Status**: in progress
- **Priority**: high
- **Completion**: 72%

## Key Objectives
No objectives defined

## Timeline
- **Start Date**: 2026-03-15
- **Target Date**: 2026-05-31

## Content
# Stratafy Experts — Roster, Linking & Context Packaging

## Overview

This initiative covers the full expert lifecycle: identity (who are the experts), mapping (what strategies do they own), and context delivery (what do they see when activated). The expert context path is architecturally separate from the general agent context path.

## Status Summary

Infrastructure is built. Expert context filtering now live in workspace snapshot. Personal Intelligence system shipped. Strategy assignments and full get_expert_context tool remain.

## Recent Progress (Mar 15–22)

**Personal Intelligence System** — New subsystem shipped: user context, lens (primary/secondary), and role context now captured per user. This feeds into expert context by understanding WHO is using the expert plugin, not just WHICH expert is active. 3 database tables, service layer, API endpoints, and MCP tool (`get_user_context`) all live.

**Expert Context Filtering** — Ownership-aware context filtering wired into `get_workspace_snapshot`. When a request comes from an expert plugin (identified via `_source_plugin`), the snapshot is now filtered to show only strategies owned by that expert at appropriate depth. This is the foundation for `get_expert_context` — the filtering logic exists, it just needs to be packaged into a dedicated tool.

**MCP Session Context** — User personal context (chapter, values, forward anchor, role mandate) now injected into MCP session instructions automatically. Optimized to fetch only on session init, not every request.

### Commits

| Commit | What |
|---|---|
| `c49c3167` | Personal Intelligence system — user context, lens, and role context |
| `9a430e28` | User context from org position → team → expert matrix |
| `39d30a53` | Expert context filtering via _source_plugin |
| `01c21498` | Ownership-aware expert context filtering |
| `665abc09` | Wire expert context filtering into get_workspace_snapshot |
| `c34ac42c` | Add strategies to snapshot context filtering sectionMap |
| `fa5286fc` | Inject user personal context into MCP session instructions |
| `36a1e176` | Add get_user_context tool (was missing from deployment) |
| `4353745b` | Add get_user_context tool, revert log_activity to simple |
| `12a5b3ca` | Return personal context on command_usage log_activity calls |
| `9a6f91b0` | Only fetch personal context on session init, not every request |
| `0c6193ba` | Add expert context filtering test scripts |
| `7231f176` | Resolve TS errors in Personal Intelligence service |

### What's Done (Updated March 22, 2026)

| Deliverable | Status |
|---|---|
| `stratafy_experts` database table | ✅ Live — 11 roles per workspace, RLS, constraints, audit fields |
| `stratafy_expert_id` FK on strategies | ✅ Live |
| Service layer (ExpertService) | ✅ Shipped |
| 7 MCP tools | ✅ Deployed |
| Tool permissions | ✅ Configured |
| Default roster seeded | ✅ Done |
| Context profiles table + resolution chain | ✅ Live |
| Context matrix UI | ✅ Live |
| Context preview UI | ✅ Live |
| AI executive roles in ws_roles | ✅ Seeded |
| Personal Intelligence system | ✅ NEW |
| Expert context filtering in snapshot | ✅ NEW |
| User context in MCP sessions | ✅ NEW |

### What Remains

| Deliverable | Status | Target |
|---|---|---|
| Assign experts to strategies | 🔲 Not started | March 2026 |
| Build `get_expert_context(role)` MCP tool | 🟡 Foundation laid | April 2026 |
| Wire context_profiles into expert context | 🔲 Not started | April 2026 |
| CTO and CSIO plugins deepened | 🟡 CTO /engage uses expert data | May 2026 |

## Success Criteria
- ✅ Full expert roster defined
- 🔲 All active strategies have a Stratafy Expert assigned
- ✅ Data model supports `stratafy_expert_id`
- 🟡 `get_expert_context(role)` — filtering foundation built
- 🔲 Context profiles wired into expert context generation
- 🟡 CTO /engage uses get_expert_strategies
