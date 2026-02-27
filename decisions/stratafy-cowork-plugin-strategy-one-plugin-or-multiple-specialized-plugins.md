---
id: 1e338886-4c64-4e4b-b64e-7dff9db1b9d2
type: decision
decisionType: type_2_reversible
status: decided
decidedAt: 2026-02-26T08:31:12.162+00:00
lastUpdated: 2026-02-27T16:56:24.118957+00:00
---

# Stratafy Cowork Plugin Strategy: One Plugin or Multiple Specialized Plugins?

## Description
With Claude Cowork plugins now available (research preview for paid users), we need to decide our plugin strategy. Stratafy already has a production MCP server with 135+ tools across strategy, insights, risks, signals, decisions, OKRs, radar, documents, teams, and more. The question is how to package this for Cowork users.

## Key Questions

1. Do we build one unified "Stratafy" plugin or multiple role-specific plugins (e.g. stratafy-coach, stratafy-ceo, stratafy-ops)?
2. If multiple, what's the sequencing?
3. What skills, commands, and sub-agents should each plugin contain?
4. How do we leverage the existing MCP server vs. creating plugin-specific experiences?

## Context

Strategy coaches are an active GTM channel showing early traction. We also have VC engagement (Madrona, Sequoia) and direct customer use cases (STIR Collective). The plugin directory is a new distribution channel — first strategy platform there wins category positioning.

## Technical Foundation

Our MCP server supports streamable HTTP, multiple auth modes (API key, OAuth, agent tokens), and is already deployed at `/api/mcp`. Plugin creation is primarily content authoring (markdown skills, markdown commands, JSON manifest).

## Details
- **Type**: Type 2 (Reversible)
- **Status**: decided
- **Authority**: Not specified
- **Deadline**: No deadline
- **Decided At**: 2026-02-26T08:31:12.162+00:00

## Context
No context recorded

## Research
See linked documents:

- **"Cowork Plugin Strategy: Research & Recommendation"** — market analysis of 15 Anthropic plugins + 4 partner plugins
- **"Stratafy User Personas"** — four-persona model: Employee, Strategy Team, Coach, External Advisor

Research showed Anthropic uses role-based plugins while partners use one-per-product. Stratafy is a product (like Slack), so the partner pattern applies — but the skill and command design must be coach-first given our GTM.

## Decision
Build one unified "stratafy" plugin designed **coach-first**. Not a separate coach plugin, not a generic company plugin — a single plugin whose skills, commands, and narrative are written from the coach's perspective, where company-facing features emerge as a natural subset.

The coach-first design reflects our GTM reality: coaches are our first users, they build their own strategies in Stratafy, then onboard clients. Every downstream persona (employee, strategy team, advisor) arrives through a coach. What works for coaches also works for everyone else — a `session-debrief` command serves a CEO debriefing a board meeting just as well as a coach debriefing a client session.

## Plugin Structure

- **6 Skills:** strategy-foundations, workspace-builder, coaching-facilitation, execution-tracking, signal-intelligence, strategic-reporting
- **6 Commands:** `setup-workspace`, `session-debrief`, `pulse`, `strategy-review`, `radar-scan`, `decision-brief`
- **Single MCP connector** pointing to the existing Stratafy API

## Split Criteria

Split into two plugins (extracting `stratafy-coach`) only if real usage data shows the unified approach hurts a specific persona — most likely when coaches need portfolio-level cross-workspace features that create noise for single-workspace users.

## Rationale
Three factors drove this decision:

1. **GTM sequence dictates plugin sequence.** Coaches are the beachhead — they arrive first, build their own workspace, then bring clients. Building a company-facing plugin first and coach plugin second would be building for users we don't have yet.

2. **Persona analysis confirms single-plugin viability.** The four user types (employee, strategy team, coach, advisor) split into single-workspace vs multi-workspace users. Three of four personas operate in one workspace and are well served by contextual skill activation within a single plugin. Only the coach is multi-workspace, but their core needs (workspace setup, strategy review, session debrief) also serve single-workspace users naturally.

3. **Partner pattern alignment.** The partner pattern in the Cowork ecosystem (Slack, Apollo, Common Room) is one plugin per product. Coaches installing one plugin with zero friction is better than coaches installing stratafy + stratafy-coach. The plugin boundary should match the product boundary, not the persona boundary.

## Outcome
No outcome recorded yet
