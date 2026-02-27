---
id: 3a003b65-925c-4738-858f-cb68526427d9
type: initiative
status: active
priority: critical
strategy: Product Architecture
completionPercentage: 0
lastUpdated: 2026-02-26T08:36:26.859+00:00
owner: af04d126-d28a-43a7-be8b-0c9451873f1b
---

# Build Stratafy Cowork Plugin

## Description
Build and ship a unified coach-first "stratafy" plugin for Claude Cowork, positioning Stratafy as the strategic context layer inside every enterprise Cowork deployment. Coaches are the primary GTM channel — they build their own strategies first, then onboard 5-20 client companies each. By designing for coaching workflows, we serve all four user personas (Coach, Strategy Team, Employee, External Advisor) because coaching workflows are a superset of company workflows. Stratafy's existing 135+ MCP tools make this primarily a packaging exercise. The plugin enriches every other Cowork plugin by injecting strategic alignment into all knowledge work.

## Parent Strategy
[Product Architecture](../strategy/functional/product-architecture.md)

## Status & Progress
- **Status**: active
- **Priority**: critical
- **Completion**: 0%

## Key Objectives
No objectives defined

## Timeline
- **Start Date**: 2026-02-25
- **Target Date**: 2026-04-08

## Content
## Decision

One unified "stratafy" plugin designed coach-first. See [Decision Record](decision:1e338886-4c64-4e4b-b64e-7dff9db1b9d2) and [Research Document](document:73940863-cd05-4896-aa42-6dfc45e61644).

## Plugin Structure (6 Skills + 6 Commands)

```
stratafy/
├── .claude-plugin/plugin.json
├── .mcp.json
├── commands/
│   ├── setup-workspace.md
│   ├── session-debrief.md
│   ├── pulse.md
│   ├── strategy-review.md
│   ├── radar-scan.md
│   └── decision-brief.md
├── skills/
│   ├── strategy-foundations/SKILL.md
│   ├── workspace-builder/SKILL.md
│   ├── coaching-facilitation/SKILL.md
│   ├── execution-tracking/SKILL.md
│   ├── signal-intelligence/SKILL.md
│   └── strategic-reporting/SKILL.md
└── settings.local.json
```

## Skills

| Skill | Primary Persona | Purpose |
|---|---|---|
| strategy-foundations | All | What strategy is, how Stratafy works, where things live |
| workspace-builder | Coach, Strategy Team | Creating, populating, and structuring workspaces |
| coaching-facilitation | Coach | Session methodology, client communication, multi-workspace patterns |
| execution-tracking | Strategy Team, Coach | OKRs, metrics, progress monitoring, assumption validation |
| signal-intelligence | Strategy Team, Coach | Signal pipeline from detection to routing, radar operations |
| strategic-reporting | All | Communicating strategic state to different audiences |

## Commands

| Command | Primary Persona | Also Serves |
|---|---|---|
| /stratafy:setup-workspace | Coach | Strategy Team |
| /stratafy:session-debrief | Coach | Strategy Team (board/meeting debriefs) |
| /stratafy:pulse | Employee | All |
| /stratafy:strategy-review | Strategy Team | Coach, Advisor |
| /stratafy:radar-scan | Strategy Team | Coach |
| /stratafy:decision-brief | Advisor | Strategy Team, Coach |

## Technical Architecture

Stratafy already has 135+ MCP tools covering the full strategic architecture: foundation, strategies, initiatives, objectives, metrics, risks, assumptions, decisions, insights, radar, reviews, documents, and agents. The plugin wraps this in Cowork's format.

Cowork plugins are markdown and JSON — no compiled code, no infrastructure. Skills = markdown domain expertise. Commands = slash commands. Connectors = .mcp.json pointing to existing MCP endpoint.

Claude's contextual skill activation means one plugin serves all four personas without overwhelming any of them. An employee asking "what's the current focus?" triggers strategy-foundations. A coach saying "I just finished a session" triggers coaching-facilitation + workspace-builder. Same plugin, different experience.

## Cross-Plugin Architecture

Stratafy's skills fire across ALL other plugins. Sales plugin drafting outreach? Strategy-foundations provides alignment context. Product plugin writing specs? Execution-tracking surfaces strategic objectives. This cross-plugin enrichment creates infrastructure positioning.

## Coach-First GTM Sequence

1. Coach installs plugin, connects API key to their own workspace
2. Coach builds their own strategy using setup-workspace and strategy-review
3. Coach uses session-debrief after client sessions to populate client workspaces
4. Client strategy teams start using pulse, strategy-review, radar-scan directly
5. Client employees use pulse for orientation
6. External advisors get invited in, use decision-brief

## Phased Delivery

**Phase 1 — Coach MVP (by March 11):** Plugin manifest, .mcp.json, 2 coach-first skills (coaching-facilitation + workspace-builder), 2 commands (/stratafy:setup-workspace + /stratafy:session-debrief), strategy-foundations skill, internal testing with Leonard's workspace.

**Phase 2 — Full Plugin (by March 25):** All 6 skills, all 6 commands, test with STIR workspace and 2-3 coaches, document cross-plugin patterns.

**Phase 3 — Marketplace Ready (by April 8):** Documentation, demo video, submit to Anthropic marketplace, apply for partner ecosystem.

**Phase 4 — Enterprise Distribution (April-May):** Private marketplace support, advisory firm distribution, PwC/Thomson Reuters exploration, Anthropic co-development conversation.

## Competitive Moat

Why consultancies can't easily replicate: no MCP infrastructure (135+ tools), no structured queryable data model, no cross-client intelligence, no real-time context. Their strategy work lives in PowerPoint.

## When to Split

Monitor adoption data for signals that the unified approach creates friction. Split triggers: plugin exceeds 10 skills, coach features confuse employees, marketplace positioning requires separate entries. The architecture allows extracting coaching skills into a separate plugin later without breaking existing users.

## Success Criteria

- Plugin functional in Cowork by March 11 (internal, coach-first features)
- External beta with 3+ coaches by March 25
- Listed in Cowork marketplace by April 8
- Referenced in Sequoia pitch as platform ecosystem play
- 1+ advisory firm distributing plugin by June
