---
id: d3fbcbb8-2e51-40da-b9de-5979a4fa7073
type: insight
source: stratafy_chat
category: product
impactLevel: medium
confidenceLevel: confirmed
status: pending
actionable: true
lastUpdated: 2026-02-08T09:15:12.986603+00:00
---

# MCP error messages are opaque and unrecoverable

## Summary
add_member returned "Database error" with no details. In conversational workflows, opaque errors are worse than in UI — no visual context to help diagnose. MCP tools need descriptive, actionable error messages.

## Description
The workspace MCP add_member tool failed with a generic "Database error" — no details, no actionable information. This is one example of a broader pattern: MCP error messages don't give enough information to diagnose or recover. In a conversational workflow, opaque errors are worse than in a UI because there's no visual context to help the user understand what happened. MCP tools need error messages that explain what went wrong and suggest what to try next.

## Classification
- **Source**: stratafy chat
- **Category**: product
- **Impact**: medium
- **Confidence**: confirmed
- **Status**: pending
- **Actionable**: Yes
- **Tags**: mcp, error-handling, developer-experience, bug-pattern


