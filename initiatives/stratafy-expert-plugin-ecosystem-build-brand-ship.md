---
id: 3a003b65-925c-4738-858f-cb68526427d9
type: initiative
status: in_progress
priority: critical
strategy: Product Architecture
completionPercentage: 70
---

# Stratafy Expert Plugin Ecosystem — Build, Brand & Ship

## Description
Build, brand, and ship the Stratafy Expert plugin ecosystem for Claude Code — 11 plugins covering a full fractional AI leadership team. Each expert is grounded in the customer's live workspace via 169+ MCP tools, owns specific strategies, and activates via slash commands. The ecosystem includes 2 non-expert plugins (Team, Guardian) and 9 expert plugins (CTO, CFO, CMO, CRO, CPO, CHRO, CoS, GC, Advisor). Published to the Claude Code plugin marketplace at github.com/Stratafy-ai/stratafy-plugins.

## Parent Strategy
[Product Architecture](../strategy/product/product-architecture.md)

## Status & Progress
- **Status**: in progress
- **Priority**: critical
- **Completion**: 70%

## Key Objectives
No objectives defined

## Timeline
- **Start Date**: 2026-02-25
- **Target Date**: 2026-05-31

## Content
## Current State (March 2026)

### Plugin Ecosystem — Live & Published

The original single "stratafy" plugin has evolved into a full ecosystem of 11 plugins with 57 commands, published to the Claude Code marketplace via `github.com/Stratafy-ai/stratafy-plugins`.

### Tier 1: Mature Plugins

| Plugin | Version | Commands | Skills | Status |
|--------|---------|----------|--------|--------|
| **stratafy-guardian** | v2.0.1 | 9 | 7 | Mature |
| **stratafy-team** | v0.9.2 | 10 | 7 | Stable |
| **stratafy-expert-cfo** | v0.4.0 | 8 | 4 | Stable |
| **stratafy-expert-cos** | v0.2.0 | 7 | 5 | Stable |

### Tier 2: Beta Plugins (with /engage command)

| Plugin | Version | Commands | Skills | Status |
|--------|---------|----------|--------|--------|
| **stratafy-expert-cto** | v0.2.1 | 7 | 0 | Beta — deepened with engage, status, tech-debt-review, build-vs-buy, risks |
| **stratafy-expert-cmo** | v0.2.0 | 3 | 0 | Beta |
| **stratafy-expert-cro** | v0.2.0 | 3 | 0 | Beta |
| **stratafy-expert-cpo** | v0.2.0 | 3 | 0 | Beta |
| **stratafy-expert-chro** | v0.2.0 | 3 | 0 | Beta |
| **stratafy-expert-gc** | v0.2.0 | 3 | 0 | Beta |
| **stratafy-expert-advisor** | v0.2.0 | 3 | 0 | Beta |

**Totals: 11 plugins, 57 commands, 23 skills**

### Architecture Pattern (Proven)

Every expert plugin follows a consistent structure:
1. Role persona in CLAUDE.md with adaptive voice
2. `/engage` command — daily activation scoped to owned strategies
3. Domain-specific commands mapped to the role's cadence
4. Skills that teach Claude domain knowledge (Tier 1 only so far)
5. MCP access to 169+ Stratafy tools
6. Activity logging for adoption metrics

### Key Differentiator

All experts share the same strategy tree. The CFO's financial scan references the same strategies the CoS tracks initiatives against. This is one strategic intelligence layer with role-specific interfaces.

## What's Done

- [x] 11 plugins built and published to marketplace
- [x] `/engage` command added to all 9 expert plugins
- [x] CTO deepened to 7 commands (engage, status, tech-review, architecture-brief, tech-debt-review, build-vs-buy, risks)
- [x] CoS deepened to 7 commands + 5 skills
- [x] Expert-to-strategy ownership mapping live via `stratafy_expert_id`
- [x] Marketplace branding: "stratafy-expert-[role]" naming convention
- [x] `marketplace.json` configured and working
- [x] MCP permissions configured for mature plugins (settings.local.json)

## What's Remaining

### Priority 1: Add skills to beta plugins
- Each beta plugin has commands but no skills — Claude has no domain knowledge for these roles
- At minimum 1 domain skill per plugin to improve output quality
- CTO, CMO, CHRO are highest priority based on customer demand

### Priority 2: Add settings.local.json to beta plugins
- 7 beta plugins missing MCP permissions config
- Users get prompted for every MCP tool call without it
- Quick fix: add `{"permissions": {"allow": ["mcp__stratafy__*"]}}` to each

### Priority 3: Deepen command sets
- Add 2-3 commands per beta plugin based on usage data
- CMO needs: positioning-workshop, competitive-landscape
- CRO needs: gtm-review, forecast
- CHRO needs: org-design (uses existing MCP org tools)
- CPO needs: prioritisation

### Priority 4: Cross-expert coordination
- Experts that reference each other's findings
- CoS as orchestration layer with `/brief` command
- Requires Hot Strategic Context Cache initiative (59dcf6b2) first

## Success Criteria

- [x] 11 plugins published to marketplace
- [x] All experts have `/engage` activation command
- [ ] All beta plugins have at least 1 domain skill
- [ ] All plugins have settings.local.json with MCP permissions
- [ ] 3+ external users actively using expert plugins
- [ ] Usage data informing command prioritisation
