---
id: 6a049139-51ce-4b93-8c68-f81e8ce0f3e7
type: initiative
status: draft
priority: high
strategy: Strategic Intelligence
completionPercentage: 0
---

# Strategic Signals — First-Class Entity & Processing Pipeline

## Description
Introduce Signals as a first-class entity — the atomic unit of strategic intelligence, decoupling detection from interpretation with a full processing pipeline.

## Parent Strategy
[Strategic Intelligence](../strategy/product/strategic-intelligence.md)

## Status & Progress
- **Status**: draft
- **Priority**: high
- **Completion**: 0%

## Key Objectives
No objectives defined

## Timeline
- **Start Date**: 2026-03-01
- **Target Date**: 2026-04-15

## Content
## Overview

Introduce Signals as a first-class entity in Stratafy's data model — the atomic unit of strategic intelligence. Signals sit upstream of every other intelligence entity (Insights, Risks, Assumptions, Decisions) and transform Stratafy from a strategic operating system you use into one that senses.

## Scope

### Core Design
- Signals decouple detection from interpretation
- Processing may produce: new risks, assumption validations/invalidations, insights, decisions, initiative impacts, or strategy review triggers
- Full provenance trail from stimulus to response via signal_routes junction table

### Pipeline
Detect -> Classify -> Research -> Assess Impact -> Route to Action

### Data Model
- New `signals` table with lifecycle: detected, classifying, researching, assessing, routed, monitoring, archived
- New `signal_routes` junction table linking signals to created/updated entities
- New `signal_strategy_links` mapping signals to affected strategies

### Phased Delivery
1. Data model + core MCP tools (2-3 days)
2. Dogfood via Claude conversations (1-2 weeks)
3. AI-assisted classification and routing prompts (2-3 weeks)
4. Automated detection sources (future)

## Expected Outcomes
- Radar findings generate Signals instead of auto-creating Insights
- Complete provenance from external event to strategic response
- MCP tools enable full signal lifecycle management
