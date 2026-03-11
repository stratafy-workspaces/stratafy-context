---
id: 3a003b65-925c-4738-858f-cb68526427d9
type: initiative
status: in_progress
priority: critical
strategy: Product Architecture
completionPercentage: 25
---

# Build Stratafy Cowork Plugin

## Description
Build and ship a unified coach-first "stratafy" plugin for Claude Cowork, positioning Stratafy as the strategic context layer inside every enterprise Cowork deployment. Coaches are the primary GTM channel — they build their own strategies first, then onboard 5-20 client companies each. By designing for coaching workflows, we serve all four user personas (Coach, Strategy Team, Employee, External Advisor) because coaching workflows are a superset of company workflows. Stratafy's existing 135+ MCP tools make this primarily a packaging exercise. The plugin enriches every other Cowork plugin by injecting strategic alignment into all knowledge work.

## Parent Strategy
[Product Architecture](../strategy/product/product-architecture.md)

## Status & Progress
- **Status**: in progress
- **Priority**: critical
- **Completion**: 25%

## Key Objectives
No objectives defined

## Timeline
- **Start Date**: 2026-02-25
- **Target Date**: 2026-03-14

## Content
## Decision

One unified "stratafy" plugin designed coach-first. See [Decision Record](decision:1e338886-4c64-4e4b-b64e-7dff9db1b9d2) and [Research Document](document:73940863-cd05-4896-aa42-6dfc45e61644).

## Current Status

Plugin is built and in active testing. Fine-tuning skills and command prompts before Brad Wilson demo (week of Feb 27). Anthropic's Feb 26 Cowork expansion (enterprise plugins, private marketplaces, 12 new connectors including Google Drive/Gmail/DocuSign) validates MCP ecosystem bet and creates urgency to be in the marketplace early.

**Priority elevation rationale:** A live Cowork plugin IS the Sequoia demo. Being in the marketplace before the pitch window is more compelling than any slide deck. The Cowork expansion makes this the highest-leverage initiative in the entire strategy tree. AGGRESSIVE TIMELINE — this is the #1 priority across all of Stratafy.

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

Stratafy already has 135+ MCP tools covering the full strategic architecture. The plugin wraps this in Cowork's format — primarily a packaging and prompt-quality exercise.

## Phased Delivery (AGGRESSIVE)

**Phase 1 — Demo-Ready Plugin (by Feb 28):** Fine-tune core skills and commands for Brad Wilson demo. Strategy-foundations + coaching-facilitation + workspace-builder skills polished. /setup-workspace and /session-debrief commands working. This is TODAY'S priority.

**Phase 2 — Full Plugin + Beta (by March 7):** All 6 skills, all 6 commands complete. Test with STIR workspace. Get 2-3 coaches using it. Document cross-plugin patterns.

**Phase 3 — Marketplace Submission (by March 14):** Documentation, demo video, submit to Anthropic marketplace. Target: listed and live before Sequoia pitch window opens.

**Phase 4 — Enterprise Distribution (March-April):** Private marketplace support, advisory firm distribution, Anthropic co-development conversation.

## Competitive Moat

Why consultancies can't easily replicate: no MCP infrastructure (135+ tools), no structured queryable data model, no cross-client intelligence, no real-time context. Their strategy work lives in PowerPoint.

## When to Split

Monitor adoption data for signals that the unified approach creates friction. Split triggers: plugin exceeds 10 skills, coach features confuse employees, marketplace positioning requires separate entries.

## Success Criteria

- Plugin demo-ready by Feb 28 — TOMORROW
- Used in Brad Wilson demo week of Feb 27-Mar 7
- All 6 skills + 6 commands complete by March 7
- External beta with 3+ coaches by March 7
- Listed in Cowork marketplace by March 14
- Referenced in Sequoia pitch as live platform ecosystem play
- 1+ advisory firm distributing plugin by May
