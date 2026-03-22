---
id: df9e136e-54ba-40ff-80c3-25b55449ea92
type: initiative
status: in_progress
priority: medium
strategy: Product Architecture
completionPercentage: 0
---

# Product Feedback Capture System

## Description
MCP-based feedback capture for bugs, enhancements, and questions. Low-friction logging with triage workflow and initiative linking.

## Parent Strategy
[Product Architecture](../strategy/product/product-architecture.md)

## Status & Progress
- **Status**: in progress
- **Priority**: medium
- **Completion**: 0%

## Key Objectives
No objectives defined

## Timeline
- **Start Date**: 2026-02-03
- **Target Date**: 2026-02-20

## Content
## Overview

MCP-based system for logging bugs, enhancements, and questions in the moment. Captures product friction while actively using Stratafy, with a triage workflow for prioritisation and linking to initiatives.

## Scope

- **Feedback Types**: Bug reports (with severity and reproduction steps), enhancement suggestions (with use case and impact), and questions (with context)
- **MCP Tools**: `log_bug`, `suggest_enhancement`, `ask_question`, `list_feedback`, `get_feedback`, `triage_feedback`
- **Status Workflow**: logged > triaged > planned > in_progress > done
- **Triage Process**: Review feedback, update status, link to initiatives and insights
- **Bug Fix Principle**: Write failing test, fix, prove with passing test
- **Database**: `ws_product_feedback` table with type, title, description, context (JSONB), severity, impact, status

## Expected Outcomes

- Capture product friction at the moment it occurs with zero context-switching
- Create a structured feedback pipeline from raw capture to planned work
- Ensure every bug fix includes a reproduction test for regression prevention
- Build a feedback corpus that informs product prioritisation decisions
