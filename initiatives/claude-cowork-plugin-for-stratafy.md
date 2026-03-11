---
id: 6f84731f-fde2-4c18-9654-bb5ba48d3861
type: initiative
status: draft
priority: high
strategy: Product Architecture
completionPercentage: 0
---

# Claude Cowork Plugin for Stratafy

## Description
Package Stratafy's strategic context delivery as a Claude Cowork plugin. The plugin becomes the distribution and UX layer — bundling prompt templates, agent configurations, slash commands, and skills into an installable package — while Stratafy remains the backend engine providing strategic context, MCP tools, and workspace data.

Currently, Stratafy delivers strategic prompts and context via MCP (115+ tools). A Cowork plugin would wrap this into a native Claude experience: users install the Stratafy plugin and immediately get context-aware strategic prompts, role-appropriate agent behaviors, and slash commands (e.g., /stratafy:alignment-scan, /stratafy:radar-scan) with namespace isolation and version control.

Key components to package:
- Context Packaging Engine prompt templates → Plugin skills
- Role-aware agent configurations (CEO, manager, IC) → Plugin agents
- Strategic slash commands → Plugin commands
- Auto-context injection hooks → Plugin hooks

Strategic value:
- New distribution channel for Stratafy intelligence
- Lower friction onboarding (install vs. configure MCP)
- Strengthens Sequoia pitch ("first strategy plugin for Cowork, ecosystem infrastructure for a platform you've bet billions on")
- Demonstrates integration depth with Anthropic platform

Architecture: Plugin calls Stratafy API/MCP backend — all strategic data, context generation, and intelligence still flows through Stratafy platform. The plugin is a consumption surface, not a replacement.

## Parent Strategy
[Product Architecture](../strategy/product/product-architecture.md)

## Status & Progress
- **Status**: draft
- **Priority**: high
- **Completion**: 0%

## Key Objectives
No objectives defined

## Timeline
- **Start Date**: Not set
- **Target Date**: Not set

## Content
No content available
