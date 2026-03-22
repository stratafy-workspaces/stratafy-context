---
id: 4c112c8e-7853-4ca5-a12a-76e455c493be
type: initiative
status: in_progress
priority: high
strategy: Strategic Delivery
completionPercentage: 70
---

# Agent Registry & API Key Platform

## Description
General-purpose agent registration and context delivery platform. Provides ws_agents table, API key management, template-based context generation, and the get_agent_context(agent_id) MCP tool for any external agent connecting to a Stratafy workspace. Scope narrowed from original — expert-specific context packaging moved to the Experts initiative. This initiative focuses on the platform that any agent (n8n workflows, custom GPTs, internal bots) uses to connect and receive workspace context configured at registration time.

## Parent Strategy
[Strategic Delivery](../strategy/product/strategic-delivery.md)

## Status & Progress
- **Status**: in progress
- **Priority**: high
- **Completion**: 70%

## Key Objectives
No objectives defined

## Timeline
- **Start Date**: 2026-02-03
- **Target Date**: 2026-06-30

## Content
# Agent Registry & API Key Platform

## Overview

This initiative provides the general-purpose agent platform — how any external agent connects to a Stratafy workspace, authenticates, and receives appropriately scoped context. It is architecturally separate from the Stratafy Expert context path.

## Scope Clarification (March 16, 2026)

Originally "Agent Registry & Context Packaging" — this initiative conflated expert context delivery with general agent infrastructure. Per architecture decision, the scope is now narrowed:

- **This initiative**: General agent platform (ws_agents, API keys, template-based context, get_agent_context)
- **Experts initiative** (`f50412ff`): Expert-specific context packaging (get_expert_context, context_profiles, role-based bundles)

## What's Built

| Component | Status |
|---|---|
| `ws_agents` table with full agent lifecycle | ✅ Live |
| AgentService (CRUD, revoke, API key management) | ✅ Complete |
| ContextGeneratorService (template-based generation) | ✅ Complete |
| 14 MCP tools (list/get/create/update/revoke agents, templates, context) | ✅ Live |
| `get_agent_context(agent_id)` tool | ✅ Live — returns cached or regenerated context |
| Agent token authentication for MCP | ✅ Live |
| Prompt templates with context_scope (full/strategic/operational/minimal) | ✅ Live |
| Context generation with LLM transformation option | ✅ Live |

## Context Resolution for General Agents

General agents declare their context needs at registration time, not via the role-based context_profiles system:

| Config Field | Purpose |
|---|---|
| `role_category` | Observer, analyst, executive, admin — determines base context scope |
| `context_sections` (jsonb) | Which sections to include: foundation, strategies, initiatives, metrics, etc. |
| `prompt_template_id` → template | Template with `context_scope` (full/strategic/operational/minimal) and optional `context_generation_prompt` for LLM transformation |
| `prompt_override` + `override_mode` | Agent-specific prompt customization (append/prepend/replace) |

### Four Resolution Levels (Implemented)

| Level | What's Included | Use Case |
|---|---|---|
| **Full** | Complete strategic architecture — every entity, every linkage | Comprehensive analysis, strategic planning |
| **Strategic** | Foundation + top-level strategies + key metrics | Leadership decisions, investor conversations |
| **Operational** | Specific strategies with initiatives and execution metrics | Department planning, initiative scoping |
| **Minimal** | Core values, mission, current priorities | Content generators, routine automation |

## What Remains

| Deliverable | Status | Priority |
|---|---|---|
| Richer `context_sections` configuration (filter by status, strategy tags) | 🔲 Not started | Medium |
| Agent creation UX improvements | 🔲 Not started | Low |
| Self-service agent onboarding flow | 🔲 Not started | Low — post-PMF |
| Per-agent TTL cache for context | 🔲 Not started | Medium |
| Documentation for external agent builders | 🔲 Not started | Medium |

## Relationship to Other Initiatives

- **Experts — Roster, Linking & Context Packaging** (`f50412ff`): Parallel path for known Stratafy Expert personas. Uses context_profiles instead of template-based config.
- **MCP Server Optimisation** (`836e9741`): Permission-scoped tool exposure and semantic discovery serve both agent types.
- **Hot Strategic Context Cache** (`59dcf6b2`): Performance layer that can accelerate both `get_agent_context` and `get_expert_context`.

## Success Criteria
- ✅ Agent registration and API key lifecycle operational
- ✅ Template-based context generation with 4 resolution levels
- ✅ 14 MCP tools deployed and tested
- 🔲 Richer context_sections config supporting status/tag filtering
- 🔲 Per-agent context caching with configurable staleness
- 🔲 At least 3 external agents actively using the platform
