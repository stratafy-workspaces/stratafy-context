---
id: 4252027f-ec4b-4419-bc01-8631565620e4
type: initiative
status: draft
priority: high
strategy: Strategic Intelligence
completionPercentage: 0
lastUpdated: 2026-02-18T05:54:30.763+00:00
owner: af04d126-d28a-43a7-be8b-0c9451873f1b
---

# Workspace Documents & Knowledge Store

## Description
Workspace-level document store for strategic knowledge — research reports, competitive analyses, board briefs, decision memos, radar summaries, and other work products. Private-first visibility model with context linking to strategies, initiatives, objectives, decisions, insights, and radar findings.

**Why this matters**: Currently, work products (research, analysis, reports) have no permanent home in the strategy system. They scatter across Linear issues, chat history, or get lost entirely. This feature closes the loop between intelligence capabilities (Insights, Decisions, Radar) and the knowledge artifacts they produce and consume.

**Core capabilities**:
- Document CRUD with markdown content
- Private-first visibility (private → workspace → shared)
- Context linking to any strategy object
- Semantic search via embeddings (pgvector)
- Agent-created documents attributed to human users
- Full-text and vector search for AI context injection

**Embedding layer**: Documents get chunked by markdown headings, embedded via pgvector, enabling semantic search ("show me anything about competitive landscape") and agent context injection (agents search document store before making recommendations).

**Phased delivery**:
1. Schema + CRUD + MCP tools (documents work, basic keyword search)
2. Embedding generation on create/update (background job)
3. Semantic search replaces keyword search
4. Agent context injection (agents query document store for relevant research before answering)

**Strategic value**: Compounds over time as the document store grows. Creates switching cost — the knowledge base becomes organizational memory. Enables the "share with someone" use case that multi-user workspaces need. Makes radar scans, alignment reports, and strategic analyses permanent, searchable, and linkable.

## Parent Strategy
[Strategic Intelligence](../strategy/functional/strategic-intelligence.md)

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
No content available
