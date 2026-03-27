---
id: 836e9741-c7ad-4200-a3ef-86ddbfb547af
type: initiative
status: in_progress
priority: medium
strategy: Strategic AI Infrastructure
completionPercentage: 15
---

# MCP Server Optimisation

## Description
Optimise Stratafy's MCP server layer across two dimensions: (1) Permission-scoped tool exposure — tools surfaced to a client reflect what the API key actually permits, eliminating tool calls that will fail; (2) Semantic tool discovery via a search_tools meta-tool for context-window efficiency, reducing session token cost from 12-19K to ~3K. Dimension 3 (executive context bundling) moved to the Experts — Roster, Linking & Context Packaging initiative where it belongs architecturally.

## Parent Strategy
[Strategic AI Infrastructure](../strategy/product/strategic-ai-infrastructure.md)

## Status & Progress
- **Status**: in progress
- **Priority**: medium
- **Completion**: 15%

## Key Objectives
No objectives defined

## Timeline
- **Start Date**: Not set
- **Target Date**: Not set

## Content
# MCP Server Optimisation

## Status: In Progress — 15% (March 22, 2026)

Foundational work complete: MCP server decomposed from monolith into 26 domain modules. Neither dimension (permission-scoped tools, semantic discovery) implemented yet, but modular architecture makes both feasible.

## Recent Progress (Mar 15–22)

**MCP Modularization** — 24,893-line monolith split into 26 domain-specific modules. Prerequisite for Dimension 1.

**Code Quality** — mcp-patterns lint plugin enforces consistent patterns across modular codebase.

**Claude.ai Compatibility** — Auto-inject tool annotations to unblock write operations.

### Commits
| Commit | What |
|---|---|
| `ab37892e` | Split MCP monolith into 26 domain modules |
| `8deb8ef0` | Add mcp-patterns lint plugin, standardize getMcpUserId |
| `9a685343` | Auto-inject tool annotations for Claude.ai |

## Dimension 1: Permission-Scoped Tool Exposure
- TOOL_PERMISSIONS map complete (284 lines)
- 26 modular tool files (NEW) — can filter per domain
- Missing: runtime tool-list filtering at session init

## Dimension 2: Semantic Tool Discovery
- Target: 60-70% token reduction (12-19K → 3.5-6K)
- Options: TF-IDF, pgvector semantic, or hybrid

## Success Criteria
- 🟡 MCP modularized (complete)
- 🔲 Permission-scoped tool manifest
- 🔲 search_tools meta-tool
- 🔲 60%+ token reduction
