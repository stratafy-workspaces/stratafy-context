---
id: 3a003b65-925c-4738-858f-cb68526427d9
type: initiative
status: in_progress
priority: critical
strategy: Product Architecture
completionPercentage: 72
---

# Stratafy Expert Plugin Ecosystem — Build, Brand & Ship

## Description
Build, brand, and ship the Stratafy Expert plugin ecosystem for Claude Code — 11 plugins covering a full fractional AI leadership team. Each expert is grounded in the customer's live workspace via 169+ MCP tools, owns specific strategies, and activates via slash commands. The ecosystem includes 2 non-expert plugins (Team, Guardian) and 9 expert plugins (CTO, CFO, CMO, CRO, CPO, CHRO, CoS, GC, Advisor). Published to the Claude Code plugin marketplace at github.com/Stratafy-ai/stratafy-plugins.

## Parent Strategy
[Product Architecture](../strategy/product/product-architecture.md)

## Status & Progress
- **Status**: in progress
- **Priority**: critical
- **Completion**: 72%

## Key Objectives
No objectives defined

## Timeline
- **Start Date**: 2026-02-25
- **Target Date**: 2026-05-31

## Content
## Current State (March 22, 2026)

### Plugin Ecosystem — Live & Published

11 plugins with 57 commands, published to the Claude Code marketplace via `github.com/Stratafy-ai/stratafy-plugins`.

## Recent Progress (Mar 15–22)

**Development Tooling** — Created `/stratafy-plugins` skill for plugin ecosystem development workflow.

**Lint Integration** — All custom oxlint rule messages now reference the relevant `/stratafy-*` skill.

**CTO Plugin Enhancement** — CTO `/engage` command now uses expert-to-strategy ownership data and expert context filtering from the workspace snapshot.

### Tier 1: Mature Plugins
- stratafy-guardian v2.0.1 (9 commands, 7 skills)
- stratafy-team v0.9.2 (10 commands, 7 skills)
- stratafy-expert-cfo v0.4.0 (8 commands, 4 skills)
- stratafy-expert-cos v0.2.0 (7 commands, 5 skills)

### Tier 2: Beta Plugins (with /engage)
- stratafy-expert-cto v0.2.1 (7 commands) — deepened with expert context
- 6 more: cmo, cro, cpo, chro, gc, advisor (3 commands each)

**Totals: 11 plugins, 57 commands, 23 skills**

## What's Done
- [x] 11 plugins published, [x] /engage on all experts, [x] CTO deepened to 7 commands
- [x] CoS deepened to 7 commands + 5 skills, [x] marketplace.json configured
- [x] /stratafy-plugins skill created, [x] lint rules reference skills

## What's Remaining
1. Add skills to beta plugins (CTO, CMO, CHRO highest priority)
2. Add settings.local.json to 7 beta plugins
3. Deepen command sets per beta plugin
4. Cross-expert coordination (requires Hot Context Cache)

## Success Criteria
- [x] 11 plugins published, [x] /engage on all, [x] dev skill created
- [ ] Beta plugins have domain skills, [ ] settings.local.json, [ ] 3+ external users
