---
id: 5c1ee1d7-9643-4ebd-825f-d2ee005dde2b
type: initiative
status: in_progress
priority: high
strategy: Product Architecture
completionPercentage: 0
lastUpdated: 2026-01-29T18:15:58.513+00:00
owner: af04d126-d28a-43a7-be8b-0c9451873f1b
---

# AI Visibility Dashboard

## Description
Surface existing MCP activity logs into a customer-facing dashboard. Shows what humans and AI agents are doing with strategic context—who accessed what, when, and what operations they performed.

THE PROBLEM WE'RE SOLVING:
Organizations have no visibility into what AI is doing in their name. They don't know:
- What content AI agents are accessing
- What decisions are being made
- Whether the context being used is current or stale
- What guardrails should exist

THE OPPORTUNITY:
We already log this data via MCP. Every tool call captures: user, operation, timestamp, duration, status, client, session. The instrumentation exists—we just need to surface it.

MVP SCOPE (Phase 1 - Visibility):
- Dashboard UI on existing log data
- Filter by user, operation type, time range
- Success/error rates
- Session activity timeline
- Basic usage analytics (already in early dev)

FUTURE PHASES:
- Phase 2: Context Audit Trail — log what context was served, alert on stale context
- Phase 3: Guardrails — define constraints, enforce at MCP layer, log violations

WHY THIS MATTERS FOR MVP:
Completes the story: Stratafy is where strategy lives AND where you see how it's being used. Without visibility, customers are flying blind. With it, we're solving a problem almost no one else is addressing.

THE PITCH:
"You're already using AI. Do you know what it's doing?"

## Parent Strategy
[Product Architecture](../strategy/functional/product-architecture.md)

## Status & Progress
- **Status**: in progress
- **Priority**: high
- **Completion**: 0%

## Key Objectives
No objectives defined

## Timeline
- **Start Date**: 2026-01-27
- **Target Date**: 2026-02-10

## Content
No content available
