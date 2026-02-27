---
id: ce3e292c-f021-4a4f-a93c-3e5e315d470c
type: initiative
status: cancelled
priority: high
strategy: AI Leverage & Automation
completionPercentage: 0
lastUpdated: 2026-02-27T16:34:37.887+00:00
owner: af04d126-d28a-43a7-be8b-0c9451873f1b
---

# Demo Prep & Outreach Agents

## Description
PAUSED: Demo Prep & Outreach Agents. Deprioritised — manual demo prep working fine for current volume. Revisit when pipeline exceeds 10 active prospects.

## Parent Strategy
[AI Leverage & Automation](../strategy/functional/ai-leverage-automation.md)

## Status & Progress
- **Status**: cancelled
- **Priority**: high
- **Completion**: 0%

## Key Objectives
No objectives defined

## Timeline
- **Start Date**: 2026-02-08
- **Target Date**: 2026-02-28

## Content
## Purpose

Automate the 3-hour-per-prospect demo prep workflow using Stratafy's own agent infrastructure. This is both operational leverage AND a proof point — Stratafy agents building Stratafy's pipeline.

## Agent: Demo Prep Agent

### What It Does
1. **Research** — Web search for company mission, vision, values, strategies from public sources
2. **Workspace Creation** — Create a new Stratafy workspace for the prospect
3. **Foundation Population** — Populate mission, vision, values, principles from research
4. **Strategy Population** — Add 2-3 key strategies and initiatives from public info
5. **Alignment Scan** — Run scan, identify genuine misalignments to surface in demo
6. **Radar Scan** — Run external scan filtered through their strategy for "aha moments"
7. **Demo Brief** — Generate a narrative: open with context, surface gaps, show radar insight

### Permissions
- Role: agent_full (read/write, no delete/admin)
- Type: assisted (human reviews all outputs before demo)
- Model: claude-sonnet-4

### Workflow
```
Leonard identifies prospect → Triggers Demo Prep Agent → Agent researches + builds workspace → Leonard reviews → Leonard adjusts → Demo ready
```

**Time saved: ~3 hours → ~30 min review per prospect**

## Agent: Outreach Drafter (Phase 2)

### What It Does
1. Takes prospect profile from Attio CRM
2. Knows Stratafy pitch angles and Leonard's tone
3. Drafts personalized outreach (email, LinkedIn, WhatsApp)
4. Tailors message to prospect's context and likely pain points

### Permissions
- Role: agent_analyst (read + cortex write)
- Type: assisted (Leonard approves before any message sent)

## Success Criteria
- Demo Prep Agent operational by Feb 15
- First automated workspace created and reviewed by Feb 16 (ScaleUp)
- 3+ prospect workspaces created by agent by Feb 28
- Time-per-workspace tracked (target: <30 min review)
- Outreach Drafter operational by Feb 20

## The Story This Tells
For investors: "I'm a solo founder who used AI agents — built on my own platform — to scale my sales pipeline from 2 prospects to 10+ in three weeks."
For customers: "This is what AI-augmented operations looks like. We built it. We use it. Now you can too."
