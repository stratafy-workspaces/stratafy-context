---
id: f50412ff-b44c-4fc3-8eee-eb31f62db598
type: initiative
status: in_progress
priority: high
strategy: Strategic Delivery
completionPercentage: 60
---

# Stratafy Experts — Roster, Linking & Context Packaging

## Description
Define the full Stratafy Expert roster, map each AI expert to their owned strategies, and build the expert-specific context delivery path. Includes: (1) Expert roster with 11 roles seeded per workspace, (2) Strategy-to-expert linking via stratafy_expert_id FK, (3) get_expert_context(role) MCP tool that resolves expert → owned strategies → context_profiles depth/access → structured bundle, (4) Wiring context_profiles resolution chain into expert context generation. The expert path is separated from the general agent path — experts use role-based context profiles with deterministic scoping; general agents use template-based configuration via ws_agents.

## Parent Strategy
[Strategic Delivery](../strategy/product/strategic-delivery.md)

## Status & Progress
- **Status**: in progress
- **Priority**: high
- **Completion**: 60%

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

Infrastructure is built. Strategy assignments, the new `get_expert_context` tool, and context profile wiring remain.

### What's Done (March 16, 2026)

| Deliverable | Status |
|---|---|
| `stratafy_experts` database table | ✅ Live — 11 roles per workspace, RLS, constraints, audit fields |
| `stratafy_expert_id` FK on strategies | ✅ Live — sits alongside `lead_id` (human) and `team_id` (human team) |
| Service layer (ExpertService) | ✅ Shipped — CRUD, assign/unassign strategy, seed roster, get by role |
| 7 MCP tools | ✅ Deployed — list_experts, get_expert, update_expert, assign/unassign, get_expert_strategies, seed_expert_roster |
| Tool permissions | ✅ Configured — read tools use strategy:read, write tools use workspace:admin or strategy:write |
| Default roster seeded to all workspaces | ✅ Done — CTO, CSIO, FD, Guardian active; rest planned |
| Naming decision | ✅ "Stratafy Experts" — per CMO recommendation. Decision logged (6b41a028) |
| Context profiles table + resolution chain | ✅ Live — 5-level priority resolution (human override → AI suggestion → filter rule → type default → role default) |
| Context matrix UI | ✅ Live — /context-profiles page with inline editing, entity drill-down, per-role depth/access |
| Context preview UI | ✅ Live — /context-profiles/preview with token budget visualization and entity-level breakdown |
| AI executive roles in ws_roles | ✅ Seeded — 10 roles with domain, token_budget, default_depth, default_access |

### What Remains

| Deliverable | Status | Target |
|---|---|---|
| Assign experts to strategies using ownership map | 🔲 Not started | March 2026 |
| Build `get_expert_context(role)` MCP tool | 🔲 Not started | April 2026 |
| Wire context_profiles resolution into expert context generation | 🔲 Not started | April 2026 |
| Update strategy content to use "Experts" language | 🔲 Not started | March 2026 |
| CTO and CSIO plugins deepened and linked | 🔲 Not started | May 2026 |

## The Expert Roster

| Role | Full Title | Status | Plugin |
|---|---|---|---|
| **CTO** | Chief Technology Officer | Active | stratafy-expert-cto v0.2.1 |
| **CSIO** | Chief Strategic Intelligence Officer | Active | stratafy-guardian v2.0.0 |
| **FD** | Finance Director | Active | stratafy-expert-cfo v0.4.0 |
| **Guardian** | Strategy Guardian | Active | stratafy-guardian v2.0.0 |
| **CMO** | Chief Marketing Officer | Planned | stratafy-expert-cmo v0.2.0 |
| **CRO** | Chief Revenue Officer | Planned | stratafy-expert-cro v0.2.0 |
| **COO** | Chief Operating Officer | Planned | stratafy-expert-coo v0.2.0 |
| **CHRO** | Chief Human Resources Officer | Planned | stratafy-expert-chro v0.2.0 |
| **CoS** | Chief of Staff | Planned | stratafy-expert-cos v0.2.0 |
| **GC** | General Counsel | Planned | stratafy-expert-gc v0.2.0 |
| **Advisor** | External Startup Advisor | Planned | stratafy-expert-advisor v0.2.0 |

## Strategy Ownership Map

| Expert | Strategies Owned |
|---|---|
| **CTO** | Product Architecture (shared with Founder), Strategic AI Infrastructure, Pulse, InsightSync, Partner Plugin Ecosystem (product), Stratafy Experts |
| **CSIO** | Strategic Intelligence |
| **FD** | Funding & Growth, Fundraising Playbook |
| **CMO** | Category Creation, SEO Strategy, StratMD Open Specification, Category Leadership |
| **CRO** | GTM Channels, Product-Market Fit, Coach Network GTM, Advisory Firms, VC as Customer, Fractional Executive & CSIO Channel, Partner Ecosystem Channel |
| **COO** | AI Leverage & Automation |
| **CHRO** | Team & Co-founder |
| **CoS** | Cross-cutting — supports all, owns none |

## Expert Context Packaging — `get_expert_context(role)`

### The Tool

A new MCP tool that accepts a Stratafy Expert role and returns a pre-packaged, profile-scoped context bundle:

```
get_expert_context(role: "CTO")

Returns:
{
  expert: { role, name, title, status },
  owned_strategies: [...],           // strategy trees filtered to owned strategies only
  active_initiatives: [...],         // initiatives under owned strategies
  health_alerts: [...],              // pre-computed health alerts across owned strategies
  overdue_items: [...],              // initiatives past target date
  stalled_items: [...],              // in_progress initiatives with no update in 14+ days
  pending_decisions: [...],          // decisions linked to owned strategies
  cross_strategy_dependencies: [...] // dependencies between owned and non-owned strategies
}
```

### How It Works

1. Resolve `role` → `stratafy_experts` record for the workspace
2. Query `strategies` where `stratafy_expert_id` = expert's ID → owned strategies
3. For each entity type, apply `context_profiles` resolution chain to determine depth/access
4. Assemble structured bundle with the resolved depth for each entity
5. Return structured JSON (not markdown) — let the consuming plugin format as needed

### Architectural Separation from General Agents

| Dimension | Expert Path | General Agent Path |
|-----------|------------|-------------------|
| Identity | `stratafy_experts` table | `ws_agents` table |
| Context scoping | `context_profiles` matrix (role-based depth/access) | `context_sections` + template config on agent record |
| Tool | `get_expert_context(role)` | `get_agent_context(agent_id)` |
| Output format | Structured JSON bundle | Rendered markdown (template-based) |
| Cacheability | High — role + workspace = deterministic key | Medium — agent-specific TTL |
| Consumer | Cowork plugins (known slash commands) | Any external agent (unknown use case) |

## Data Model (Completed)

Table: `stratafy_experts`
- Identity: role (enum), name, title, slug, description, status
- Prompts: system_prompt, persona_prompt
- Context: context_sections (jsonb), tool_scopes (jsonb)
- Links: prompt_template_id → ws_context_prompt_templates, agent_id → ws_agents
- Metadata: plugin_version, avatar_url, position
- Constraint: unique (workspace_id, role) — one expert per role per workspace

Strategy link: `strategies.stratafy_expert_id` FK → `stratafy_experts.id`

## Related Decisions
- Decision `6cbd56ba` — Strategy-to-expert linking: support named AI experts as strategy owners
- Decision `6b41a028` — Rename from "The Stratafy Team" to "Stratafy Experts"

## Success Criteria
- ✅ Full expert roster defined with plugin specs for each role
- 🔲 All active strategies have a Stratafy Expert assigned
- ✅ Data model updated to support `stratafy_expert_id` field on strategies
- 🔲 `get_expert_context(role)` tool live and returning structured bundles
- 🔲 Context profiles resolution chain wired into expert context generation
- 🔲 At least CTO and CSIO plugins using `get_expert_context` instead of sequential `get_strategy_tree` calls by May 2026
