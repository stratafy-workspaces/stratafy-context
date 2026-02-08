---
id: 281cac3a-e1a0-4e48-a9f8-90be72b1c325
type: initiative
status: in_progress
priority: high
strategy: AI Leverage & Automation
completionPercentage: 0
lastUpdated: 2026-01-29T09:21:06.830929+00:00
owner: af04d126-d28a-43a7-be8b-0c9451873f1b
---

# CRM Automation Setup

## Description
Transform Attio from static database to AI-augmented CRM. Implement post-meeting note capture, automated next-action suggestions, pipeline stage recommendations, and weekly AI-powered pipeline reviews. First test of systematic AI automation in operations.

## Parent Strategy
[AI Leverage & Automation](../strategy/functional/ai-leverage-automation.md)

## Status & Progress
- **Status**: in progress
- **Priority**: high
- **Completion**: 0%

## Key Objectives
No objectives defined

## Timeline
- **Start Date**: 2026-01-30
- **Target Date**: 2026-02-20

## Content
# CRM Automation Setup

## Purpose

Transform Attio from a static database into an AI-augmented relationship management system. Every interaction should flow into the CRM with minimal manual effort.

## Current State Problems

1. **Post-meeting updates forgotten** — Context from conversations lives in memory, not system
2. **Pipeline stages stale** — Manual updates lag reality
3. **No strategic context in CRM** — Attio doesn't know about Stratafy insights
4. **Notes are empty** — Key relationships (ScaleUp Company, Clickatell, Sequoia path) have zero documented context

## Target State

| Workflow | Before | After |
|----------|--------|-------|
| After a call | Nothing captured | AI drafts note + next action in Attio |
| Weekly review | Manual pipeline scan | AI surfaces stale deals, suggests actions |
| Meeting prep | Manual research | AI pulls context from Attio + Stratafy |
| Contact research | Manual googling | AI enriches with web research |

## Implementation

### Phase 1: Foundation (Week 1)

- [ ] Add strategic context notes to key prospects (ScaleUp, Clickatell, African Green Alpha)
- [ ] Restructure pipeline stages to match actual sales motion
- [ ] Add custom fields: Lighthouse Potential, Demo Approach, Strategic Value
- [ ] Clean up duplicate entries

### Phase 2: Capture Workflows (Week 2)

- [ ] Create post-meeting prompt template for Claude
- [ ] Test: After next call, use Claude + Attio MCP to update record
- [ ] Document the workflow that works
- [ ] Set calendar reminder to trigger after every external call

### Phase 3: Review Workflows (Week 3)

- [ ] Create weekly pipeline review prompt
- [ ] AI scans all deals, flags: stale (no update 7+ days), missing next action, missing notes
- [ ] Human reviews AI suggestions, approves updates
- [ ] Track time saved vs. manual review

## Success Criteria

| Metric | Target |
|--------|--------|
| % of meetings with CRM notes | >80% |
| Average time from meeting to CRM update | <1 hour |
| Deals with current next actions | >90% |
| Time spent on manual CRM updates | -50% |

## Tools Required

- Attio MCP (already connected)
- Claude with Attio access
- Calendar integration for meeting triggers

## Risks

| Risk | Mitigation |
|------|------------|
| AI captures inaccurate info | Human reviews all AI-drafted notes before save |
| Workflow too complex | Start with simplest version, iterate |
| MCP unreliable | Document manual fallback |
