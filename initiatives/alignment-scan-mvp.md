---
id: 0327f9f0-3b69-4a0f-a35a-644ff10860d9
type: initiative
status: in_progress
priority: critical
strategy: Product-Market Fit
completionPercentage: 0
lastUpdated: 2026-02-11T09:46:42.037+00:00
owner: af04d126-d28a-43a7-be8b-0c9451873f1b
---

# Alignment Scan MVP

## Description
Ship Foundation Alignment perspective within existing Strategy Reviews system. AI-powered analysis that checks strategies against mission, vision, values, beliefs, and principles. Parallel execution for speed. Being finalised alongside STIR onboarding (week of Feb 17) — STIR's real strategy data provides the ideal test environment. Demo-ready for ScaleUp Company meeting on Feb 23.

## Parent Strategy
[Product-Market Fit](../strategy/functional/product-market-fit.md)

## Status & Progress
- **Status**: in progress
- **Priority**: critical
- **Completion**: 0%

## Key Objectives
No objectives defined

## Timeline
- **Start Date**: 2026-01-27
- **Target Date**: 2026-02-21

## Content
# Alignment Scan MVP

## Purpose

Ship the Foundation Alignment perspective within the existing Strategy Reviews system. This is the core Stratafy value proposition: **AI that checks whether your strategies actually align with who you say you are.**

Demo-ready for ScaleUp Company pilot in 2 weeks.

## Strategic Alignment

- **Parent Strategy**: Product-Market Fit
- **Validates**: A1 (value hook), A9 (alignment scoring adds value), A10 (AI can detect gaps)
- **Supports**: "Explainability is non-negotiable" (Principle #3)
- **Proves**: The core thesis — strategy must be consumable by AI to be governed by AI

## What It Does

### Foundation Alignment Perspective

A new perspective type (`foundation_alignment`) that evaluates strategies against:

| Element | Check | Output |
|---------|-------|--------|
| **Mission** | Does this strategy advance the mission? | Score (1-10) + explanation |
| **Vision** | Does this strategy move toward the vision? | Score (1-10) + explanation |
| **Values** | Which values does this support/contradict? | Mapping + gaps + conflicts |
| **Beliefs** | Is this consistent with stated beliefs? | Alignment + contradictions |
| **Principles** | Does the approach follow stated principles? | Compliance + violations |

### SWOT Output

For each strategy scanned:

- **Strengths**: Strong alignment areas, well-connected to foundation
- **Weaknesses**: Gaps, contradictions, orphaned from identity
- **Opportunities**: Implicit connections that should be made explicit
- **Threats**: Drift risk, principle violations, value conflicts

### Scoring

- Overall alignment score (1-10, weighted average)
- Per-element scores (mission, vision, values, beliefs, principles)
- Confidence level (low/medium/high based on data completeness)

## Technical Approach

### Architecture

```
┌─────────────────┐     ┌──────────────────┐     ┌─────────────────┐
│  Trigger Scan   │────▶│  Parallel API    │────▶│  Store Results  │
│  (UI or MCP)    │     │  Calls (Claude/  │     │  (Reviews DB)   │
│                 │     │  Grok)           │     │                 │
└─────────────────┘     └──────────────────┘     └─────────────────┘
```

### Parallel Execution

To scan a workspace quickly:

1. Fetch all strategies in workspace
2. Fetch full foundation (mission, vision, values, beliefs, principles)
3. For each strategy, spawn parallel AI calls:
   - One call per strategy (or batch if context allows)
   - Each call receives: strategy + full foundation context
4. Collect results, store as review perspectives
5. Calculate overall scores

**Target**: Scan 10 strategies in <30 seconds (parallel API calls)

### AI Prompt Structure

```
You are evaluating strategic alignment for an organization.

## Foundation (Who They Are)
Mission: {mission}
Vision: {vision}
Values: {values with content}
Beliefs: {beliefs with content}
Principles: {principles with content}

## Strategy Being Evaluated
Name: {strategy name}
Description: {description}
Content: {full content}
Parent Strategy: {if exists}
Child Strategies: {if exist}
Initiatives: {if exist}

## Your Task
Evaluate how well this strategy aligns with the foundation.

For each element (mission, vision, values, beliefs, principles):
1. Score alignment 1-10
2. Explain your reasoning
3. Flag any contradictions or gaps

Then provide:
- Overall alignment score (weighted average)
- Top 3 strengths
- Top 3 weaknesses  
- Top 3 opportunities to strengthen alignment
- Top 3 risks/threats from misalignment
- Specific recommendations

Respond in JSON format: {schema}
```

### API Integration

- **Claude API**: Primary for nuanced analysis
- **Grok API**: Backup / parallel for speed
- Both return structured JSON parsed into perspective records

## Scope

### In Scope (2 weeks)

| Task | Days | Notes |
|------|------|-------|
| Add `foundation_alignment` perspective type | 0.5 | DB migration, type updates |
| Build AI prompt + response parser | 1 | Structured output, error handling |
| Implement parallel scan orchestration | 1 | Promise.all / queue management |
| Wire up `generateAIReview` with real AI | 1 | Replace placeholder |
| Build scan trigger UI (button on strategy page) | 1 | Minimal, functional |
| Build results view UI | 2 | Show perspectives, scores, SWOT |
| Test on Stratafy workspace | 0.5 | Eat own dogfood |
| Test on ScaleUp Company workspace | 1 | Pilot prep |
| Buffer | 2 | Things always take longer |
| **Total** | **10 days** | Fits 2-week window |

### Out of Scope (Later)

- Other perspective types (market, financial, etc.) — existing placeholders stay
- MCP tools for triggering scans — use UI for now
- Scheduled/automatic scans — manual trigger only
- Cross-workspace comparisons
- Historical trend tracking

## Success Criteria

| Criteria | Target |
|----------|--------|
| Scan completes for 10 strategies | <60 seconds |
| AI produces coherent alignment analysis | Human review confirms quality |
| Scores feel accurate | Test against Stratafy workspace, validate intuition |
| ScaleUp Company finds value | "This is useful" in pilot feedback |
| Demo works reliably | No crashes, timeouts, or nonsense output |

## Risks & Mitigations

| Risk | Likelihood | Mitigation |
|------|------------|------------|
| AI output quality inconsistent | Medium | Iterate on prompt, add examples |
| API rate limits hit on parallel calls | Low | Add queuing, backoff |
| 2 weeks too tight | Medium | Cut UI polish, prioritize function over form |
| ScaleUp workspace not ready | Low | Use Stratafy workspace as backup demo |

## Dependencies

- ScaleUp Company workspace populated with their foundation + strategies
- Claude/Grok API keys with sufficient quota
- Strategy Reviews system working (✅ already built)

## Next Actions

| Action | Owner | Deadline |
|--------|-------|----------|
| Add `foundation_alignment` to perspective types | Leonard | Jan 28 |
| Draft AI prompt, test on single strategy | Leonard | Jan 29 |
| Implement parallel scan logic | Leonard | Jan 31 |
| Build trigger UI (button) | Leonard | Feb 3 |
| Build results view UI | Leonard | Feb 6 |
| Test on Stratafy workspace | Leonard | Feb 7 |
| Test on ScaleUp Company workspace | Leonard | Feb 9 |
| Demo prep / polish | Leonard | Feb 10 |

## Definition of Done

- [ ] User can click "Run Alignment Scan" on any strategy
- [ ] Scan runs against foundation, produces scored perspective
- [ ] Results display with SWOT, recommendations
- [ ] Works on ScaleUp Company workspace
- [ ] Demo takes <5 minutes and tells a clear story
