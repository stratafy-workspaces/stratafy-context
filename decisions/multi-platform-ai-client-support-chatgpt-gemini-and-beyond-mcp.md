---
id: 6277be6c-47c9-4544-a04f-3de2a6e16aac
type: decision
decisionType: type_1_irreversible
status: pending
---

# Multi-platform AI client support: ChatGPT, Gemini, and beyond MCP

## Description
Currently Stratafy's conversational interface is built exclusively on MCP (Model Context Protocol), which only works with Claude. This limits customer onboarding to Claude users — a real friction point surfaced when onboarding Viridis AFC's Gert Vermaak, who would need a Claude Pro subscription or a technical Desktop JSON setup to connect.

The decision is whether Stratafy should remain **Claude/MCP-only** or invest in building alternative integrations (OpenAI GPT Actions, Google Gemini extensions, generic REST API) to be platform-agnostic.

## Details
- **Type**: Type 1 (Irreversible)
- **Status**: pending
- **Authority**: Not specified
- **Deadline**: No deadline
- **Decided At**: Not yet decided

## Context
UPDATED Feb 27, 2026: Anthropic's Cowork expansion (Feb 26) with enterprise plugins, private marketplaces, and 12 new connectors strongly reinforces MCP-first approach. The platform is investing heavily in exactly the ecosystem we're building for. However, OpenAI's Big 4 consulting partnerships (Feb 23) introduce a monitoring trigger: if advisory firm prospects cite ChatGPT/OpenAI preference as blocker, we may need to revisit. For now, MCP-first is the right call — Cowork is becoming the enterprise AI desktop. Monitor for OpenAI preference signals from prospects.

## Research
## Alternatives Explored

1. **OpenAI GPT Actions** — REST API based, would require building a separate API layer mapping Stratafy operations to OpenAI's action schema
2. **Generic REST API** — already partially exists for MCP, could be exposed directly
3. **Gemini Extensions** — Google's equivalent, different architecture again
4. **Stay MCP-only** — bet on MCP becoming the industry standard (other clients like Cursor already adopting it)

## Key Consideration

MCP adoption is growing but not universal. ChatGPT has the largest consumer AI user base.

## Decision
Not yet decided

## Rationale
No rationale recorded

## Outcome
No outcome recorded yet
