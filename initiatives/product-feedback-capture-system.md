---
id: df9e136e-54ba-40ff-80c3-25b55449ea92
type: initiative
status: in_progress
priority: medium
strategy: Product Architecture
completionPercentage: 0
lastUpdated: 2026-02-03T12:06:09.892+00:00
owner: af04d126-d28a-43a7-be8b-0c9451873f1b
---

# Product Feedback Capture System

## Description
MCP-based system for logging bugs, enhancements, and questions in the moment. Captures product friction while using Stratafy.

**TABLE:** `ws_product_feedback`
- type (bug | enhancement | question)
- title, description, context (jsonb)
- severity (bugs), impact (enhancements)
- status workflow: logged → triaged → planned → in_progress → done
- Links to initiatives and insights

**WORKFLOW:**
1. Agent logs feedback via MCP (raw capture, low friction)
2. Leonard triages: reviews feedback, updates status, links to initiatives
3. Creates Linear issues manually when needed (integration deferred)

**MCP TOOLS:**
- `log_bug` — title, description, severity, reproduction_steps, context
- `suggest_enhancement` — title, description, use_case, impact
- `ask_question` — title, description, context
- `list_feedback` — filter by type, status
- `get_feedback` — full details
- `triage_feedback` — update status, link to initiative/insight

**BUG FIX PRINCIPLE:**
When fixing a bug: (1) Write failing test, (2) Fix, (3) Prove with passing test.

**SUCCESS CRITERIA:**
- Can log bug via MCP while working
- Can list and filter feedback by type/status
- Can triage feedback and link to initiatives
- Bug fixes include reproduction test

**DEFERRED (Future Phase):**
- Linear sync (sync_to_linear tool, bidirectional linking)
- Duplicate detection via semantic similarity
- Automated triage agent

## Parent Strategy
[Product Architecture](../strategy/functional/product-architecture.md)

## Status & Progress
- **Status**: in progress
- **Priority**: medium
- **Completion**: 0%

## Key Objectives
No objectives defined

## Timeline
- **Start Date**: 2026-02-03
- **Target Date**: 2026-02-14

## Content
No content available
