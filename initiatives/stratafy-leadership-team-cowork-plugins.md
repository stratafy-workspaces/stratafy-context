---
id: 109633b3-21f8-44b3-b9d1-e1845cc2c9bd
type: initiative
status: active
priority: critical
strategy: Strategic Delivery
completionPercentage: 0
---

# Stratafy Leadership Team — Cowork Plugins

## Description
Pre-built AI executive personas delivered as Claude Cowork plugins. Seven Stratafy executives: CFO, COO, CMO, CTO, CPO, CHRO, and CSIO (Chief Strategic Intelligence Officer). Each is a registered agent with domain expertise, strategic context, MCP tool access, and authority boundaries.

THE SEVEN EXECUTIVES:
- Stratafy CFO — Financial intelligence, strategy-finance alignment
- Stratafy COO — Operational coordination, execution tracking
- Stratafy CMO — Strategic marketing, category creation, content
- Stratafy CTO — Technical architecture, engineering strategy
- Stratafy CPO — Product management, customer insights
- Stratafy CHRO — Organisational design, people strategy
- Stratafy CSIO — Strategic intelligence orchestration (NEW ROLE). Oversees entire strategic architecture, runs cross-functional alignment scans, synthesises insights across all executives, detects compound cross-domain issues, maintains strategic health. The role Stratafy creates and defines — the Salesforce pattern applied to strategic intelligence.

NAMING: 'Stratafy [Role]' — brand qualifies the role. Collective: 'Stratafy Leadership Team.'

BUILD: (1) Stratafy CFO with Finance Module, (2) Stratafy COO from Chief of Staff, (3) Stratafy CSIO as orchestration layer, (4) Full team (CMO, CTO, CPO, CHRO), (5) Marketplace post-seed.

PACKAGING:
- Founder Team (R25k/month): CFO + COO + CMO
- Executive Team (R50k/month): Full C-suite (7 executives including CSIO)
- Advisory Executive Suite: Deploy to client workspaces with firm's methodology

MOAT: Strategic context (only Stratafy) + tool access (MCP) + authority boundaries (agent registry) + context freshness (packaging engine) + CSIO role definition (category creation). Chatbots can't replicate this.

## Parent Strategy
[Strategic Delivery](../strategy/product/strategic-delivery.md)

## Status & Progress
- **Status**: active
- **Priority**: critical
- **Completion**: 0%

## Key Objectives
No objectives defined

## Timeline
- **Start Date**: 2026-03-15
- **Target Date**: 2026-05-31

## Content
# Stratafy Leadership Team — Cowork Plugins

## Overview
Pre-built AI executive personas delivered as Claude Cowork plugins. Each executive has domain expertise, strategic context scoped to their owned strategies, MCP tool access, and a set of slash commands for daily activation.

## The Executive Roster

| Role | Owned Strategies | Plugin Status |
|---|---|---|
| **CTO** | Strategic AI Infrastructure, Product Architecture (shared), Pulse, InsightSync, Partner Plugin Ecosystem (product) | To build — priority |
| **CSIO** | Strategic Intelligence | Plugin spec exists |
| **FD / CFO** | Funding & Growth, Fundraising Playbook | Built (stratafy-finance v0.3.0) |
| **CMO** | Category Creation, SEO Strategy, StratMD | Planned Q2 2026 |
| **CRO** | GTM Channels, Product-Market Fit, all GTM sub-strategies, Partner Plugin Ecosystem (GTM) | Planned Q2 2026 |
| **COO** | AI Leverage & Automation, MVP Development | Planned Q2 2026 |
| **CHRO** | Team & Co-founder | Planned Q3 2026 — potential We Are 52 co-build |
| **CoS** | Cross-cutting — no direct ownership. Read-only. | To build after CTO + Daily Execution Loop |

## Build Sequence (Decided — Decision `8d100338`)

The build order is fixed. Do not build CoS before CTO plugin and Daily Execution Loop are live.

**1. CTO plugin + `/engage`**
Validates the single-executive activation pattern. One executive, one domain, deterministic MCP calls. Proves the concept before adding orchestration complexity.

**2. Daily Execution Loop** (`b3790ca6`)
Upstream dependency for CoS. `/brief` is only as good as the freshness of the workspace. If the workspace hasn't been updated in 3 days, the CoS will surface stale intelligence with confidence. Daily Execution Loop ensures the data is live before the orchestration layer runs.

**3. CoS + `/brief`**
Orchestration layer — sequential executive scanning, cross-executive tension detection, consolidated company briefing. Built on a proven single-executive pattern and fresh workspace data.

**4. True parallel execution (post-seed)**
Parallel API calls to each executive plugin via Anthropic API, responses collected, fed into CoS consolidation call. Faster, fully independent per-executive output. Build when agent infrastructure is in place post-seed.

## Executive Activation Commands

Each plugin exposes a standard set of slash commands. The `/engage` command is the highest-value to build first — it's the daily activation pattern that makes the executive feel like a real team member showing up for work rather than a tool you have to pull from.

### Standard Commands (all executives)

| Command | Behaviour |
|---|---|
| `/engage` | Review owned strategies, surface top 3 things needing attention, suggest one concrete next action per item — in the executive's voice |
| `/status` | Quick health check — green/amber/red per owned strategy |
| `/risks` | Pull risks and assumptions across owned strategies |

### Executive-Specific Commands

| Executive | Command | Behaviour |
|---|---|---|
| **CTO** | `/infra-status` | Current state of 7 infrastructure capabilities with completion % |
| **CTO** | `/sequence` | Validate initiative ordering — flag sequencing risks |
| **CRO** | `/pipeline` | GTM pipeline status, stalled deals, next outreach actions |
| **FD** | `/numbers` | Financial metrics, budget burn, funding progress |
| **CSIO** | `/intelligence` | Recent signals, insights, and radar findings needing attention |
| **CoS** | `/brief` | Orchestrate all executives sequentially, consolidate, surface cross-executive tensions. Read-only — no mutations. |

### How `/engage` Works

When triggered, the executive:
1. Calls `get_strategy_tree` on each owned strategy
2. Identifies overdue initiatives, health alerts, stalled items (in_progress >14 days without update)
3. Surfaces top 3 items ranked by strategic risk
4. Suggests one concrete next action per item, in the executive's domain voice
5. Flags cross-strategy dependencies at risk

**Example CTO `/engage` output:**
> "Three things need your attention this week. Strategic Evolution & Time-Travel is at 95% and has been stalled for 14 days — the remaining 5% is snapshot size optimisation and proactive causal alerting. Ship it. Hybrid Strategic Retrieval has no target date and no objectives — it's active but drifting. And the MCP Server Optimisation initiative is still on Product Architecture when it should be here. That's an ownership ambiguity that will confuse the next engineer. Recommend we move it."

---

## CoS `/brief` — Executive Orchestration Pattern

The CoS is the orchestration layer. When `/brief` is triggered, it runs through each executive's owned strategies sequentially, applies that executive's lens, and consolidates into a single company-wide briefing with cross-executive tensions surfaced.

### ⚠️ CoS is permanently read-only

The CoS sees everything but owns nothing. It cannot propose workspace mutations — no `update_strategy`, no `create_initiative`, no `update_initiative`. If the CoS identifies something that needs to change, it surfaces the recommendation and tells you which executive plugin to activate to act on it. Write authority stays with individual executive plugins, scoped to their owned strategies.

This is a governance boundary, not a technical limitation. It mirrors how a real Chief of Staff operates — they brief, synthesise, and coordinate, but they don't make unilateral changes to strategy.

### How `/brief` Works

The CoS holds all executive context in its system prompt and knows how to think like each one when scanning their strategies. From the user's perspective it feels like the CoS "called" the other executives — what's happening is sequential MCP scanning with role-specific interpretation applied at each step.

**Execution sequence on `/brief`:**

```
1. CTO lens
   → get_strategy_tree: Strategic AI Infrastructure, Pulse, InsightSync
   → Flag: overdue initiatives, stalled builds, architectural risks, sequencing issues

2. CSIO lens
   → get_strategy_tree: Strategic Intelligence
   → Flag: unrouted signals, insights without action, radar gaps, intelligence blind spots

3. FD lens
   → get_strategy_tree: Funding & Growth, Fundraising Playbook
   → Flag: fundraise timeline risks, pitch readiness gaps, metrics not tracked

4. CMO lens
   → get_strategy_tree: Category Creation, SEO Strategy, StratMD
   → Flag: content pipeline stalls, category positioning gaps, thought leadership gaps

5. CRO lens
   → get_strategy_tree: GTM Channels, Product-Market Fit, all GTM sub-strategies
   → Flag: pipeline stalls, demo readiness, customer conversion gaps, channel activation delays

6. COO lens
   → get_strategy_tree: AI Leverage & Automation, MVP Development
   → Flag: execution bottlenecks, automation wins not documented, MVP milestones at risk

7. Synthesise
   → Identify top 3 cross-executive tensions
   → Identify top 3 company-wide priorities for the week
   → Flag decisions pending too long
   → Recommend which executive to activate first and why
   → All recommendations only — no mutations
```

### Cross-Executive Tension Detection

The CoS's primary value over individual `/engage` calls is detecting tensions that no single executive would surface:

- **CRO has a demo booked** (Evolve IR, March 20) but **CTO's Cowork Plugin is 25% complete** — demo tooling may not be ready
- **FD flags fundraise window is April** but **CMO has no content pipeline active** — category narrative isn't built ahead of pitch
- **COO shows MVP at risk** but **CRO is running pipeline diversification** — promising customers before the product is stable

These compound risks are invisible to each executive individually but obvious to the CoS scanning across all domains.

### Upstream Dependencies

`/brief` quality is bounded by two upstream capabilities:

| Dependency | Initiative | Status | Risk if absent |
|---|---|---|---|
| Workspace freshness | Daily Execution Loop (`b3790ca6`) | Active | CoS surfaces stale intelligence confidently |
| Context speed | Hot Strategic Context Cache (`59dcf6b2`) | Active | Context window pressure before synthesis step |

Do not ship `/brief` until Daily Execution Loop is live and the workspace is being updated daily.

### Future: True Parallel Execution

The current pattern is sequential scanning within a single Claude session. A future capability — buildable via the Anthropic API — is genuine parallel execution: parallel API calls to each executive plugin, responses collected, fed into a CoS consolidation call. This would make `/brief` faster and each executive's output fully independent. Build post-seed when agent infrastructure is in place.

---

## Plugin Architecture

Each executive plugin requires three things:

**1. System prompt** — defines the executive's persona, domain expertise, owned strategy IDs, tone, and decision authority boundary.

**2. Slash commands** — mapped to prompt templates that trigger the right MCP calls scoped to the executive's strategies.

**3. MCP access scope:**
- Individual executives: read-wide across workspace; write restricted to owned strategies and initiatives
- CoS: read-wide across workspace; **no write access under any circumstance**

## Related Decisions
- Decision `8d100338` — Build sequence: CTO → Daily Execution Loop → CoS; CoS permanently read-only
- Decision `6cbd56ba` — Strategy-to-Stratafy Team member linking
- Decision `3d804525` — Architectural boundary: Strategic AI Infrastructure owns retrieval/assembly/delivery
