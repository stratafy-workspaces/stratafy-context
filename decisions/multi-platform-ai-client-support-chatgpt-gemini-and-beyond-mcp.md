---
id: 6277be6c-47c9-4544-a04f-3de2a6e16aac
type: decision
decisionType: type_1_irreversible
status: pending
lastUpdated: 2026-02-09T07:42:38.107366+00:00
---

# Multi-platform AI client support: ChatGPT, Gemini, and beyond MCP

## Description
Currently Stratafy's conversational interface is built exclusively on MCP (Model Context Protocol), which only works with Claude. This limits customer onboarding to Claude users — a real friction point surfaced when onboarding Viridis AFC's Gert Vermaak, who would need a Claude Pro subscription or a technical Desktop JSON setup to connect. The decision is whether Stratafy should remain Claude/MCP-only or invest in building alternative integrations (OpenAI GPT Actions, Google Gemini extensions, generic REST API) to be platform-agnostic.

## Details
- **Type**: Type 1 (Irreversible)
- **Status**: pending
- **Authority**: Not specified
- **Deadline**: No deadline
- **Decided At**: Not yet decided

## Context
MCP is Anthropic's open protocol — currently supported by Claude, Cursor, and some IDE clients but not ChatGPT or Gemini. Stratafy's entire conversational strategy layer is built on MCP. Real customer friction identified: Viridis AFC founder needs Claude Pro ($20/mo) or technical JSON config to access Stratafy. OpenAI offers GPT Actions (REST-based) and ChatGPT plugins as alternative integration paths. Building multi-platform support would require maintaining separate integration layers but would remove a significant adoption barrier.

## Research
Alternatives explored: 1) OpenAI GPT Actions — REST API based, would require building a separate API layer mapping Stratafy operations to OpenAI's action schema. 2) Generic REST API — already partially exists for MCP, could be exposed directly. 3) Gemini Extensions — Google's equivalent, different architecture again. 4) Stay MCP-only — bet on MCP becoming the industry standard (other clients like Cursor already adopting it). Key consideration: MCP adoption is growing but not universal. ChatGPT has the largest consumer AI user base.

## Decision
Not yet decided

## Rationale
No rationale recorded

## Outcome
No outcome recorded yet
