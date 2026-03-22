---
id: 4252027f-ec4b-4419-bc01-8631565620e4
type: initiative
status: draft
priority: high
strategy: Strategic Intelligence
completionPercentage: 0
---

# Workspace Documents & Knowledge Store

## Description
Workspace-level document store for strategic knowledge — research, analyses, memos — with semantic search, context linking, and agent context injection.

## Parent Strategy
[Strategic Intelligence](../strategy/product/strategic-intelligence.md)

## Status & Progress
- **Status**: draft
- **Priority**: high
- **Completion**: 0%

## Key Objectives
No objectives defined

## Timeline
- **Start Date**: 2026-02-24
- **Target Date**: 2026-04-30

## Content
## Overview

Workspace-level document store for strategic knowledge — research reports, competitive analyses, board briefs, decision memos, radar summaries, and other work products. Closes the loop between intelligence capabilities and the knowledge artifacts they produce and consume.

## Scope

### Core Capabilities
- Document CRUD with markdown content
- Private-first visibility model (private, workspace, shared)
- Context linking to any strategy object (strategies, initiatives, objectives, decisions, insights, radar findings)

### Search & Discovery
- Full-text keyword search (Phase 1)
- Semantic search via pgvector embeddings (Phase 3)
- Document chunking by markdown headings for embedding generation

### Agent Integration
- Agent-created documents attributed to human users
- Agent context injection: agents query document store before making recommendations (Phase 4)

### Phased Delivery
1. Schema + CRUD + MCP tools with basic keyword search
2. Embedding generation on create/update (background job)
3. Semantic search replaces keyword search
4. Agent context injection for AI-informed recommendations

## Expected Outcomes
- Work products have a permanent, searchable home in the strategy system
- Switching costs increase as organizational knowledge accumulates
- Agents make better recommendations by referencing existing research and analysis
