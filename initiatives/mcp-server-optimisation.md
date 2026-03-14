---
id: 836e9741-c7ad-4200-a3ef-86ddbfb547af
type: initiative
status: draft
priority: medium
strategy: Product Architecture
completionPercentage: 0
---

# MCP Server Optimisation

## Description
Optimise Stratafy's MCP server layer across two dimensions: (1) Permission-scoped tool exposure — tools surfaced to a client should reflect what the API key actually permits, eliminating tool calls that will fail due to insufficient permissions and reducing noise in the tool list; (2) Semantic tool discovery — implement a search_tools meta-tool so agents can discover capabilities dynamically rather than loading the full tool registry into context on every session. This reduces context bloat, improves agent reliability, and makes the MCP layer production-grade for multi-tenant and agent-framework integrations. Covers all active MCP servers (workspace, agents, workspace admin). Architecture decision required on embedding approach (lightweight BM25/keyword vs. full semantic embeddings) based on tool count and description quality.

## Parent Strategy
[Product Architecture](../strategy/product/product-architecture.md)

## Status & Progress
- **Status**: draft
- **Priority**: medium
- **Completion**: 0%

## Key Objectives
No objectives defined

## Timeline
- **Start Date**: Not set
- **Target Date**: Not set

## Content
No content available
