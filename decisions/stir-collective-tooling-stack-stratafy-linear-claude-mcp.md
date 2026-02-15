---
id: 0fa837ee-e92a-4d58-a0c2-044b3962dc5d
type: decision
decisionType: type_2_reversible
status: decided
decidedAt: 2026-02-10T11:36:32.97+00:00
lastUpdated: 2026-02-10T11:36:33.039962+00:00
---

# STIR Collective tooling stack: Stratafy + Linear + Claude MCP

## Description
Define the operational tooling stack for the STIR Collective customer engagement. Need to decide how strategy execution and operational execution are managed across tools.

## Details
- **Type**: Type 2 (Reversible)
- **Status**: decided
- **Authority**: Not specified
- **Deadline**: No deadline
- **Decided At**: 2026-02-10T11:36:32.97+00:00

## Context
First paying customer (STIR Collective, R25,000/month retainer) starting Feb 17. Multi-subsidiary event company needing strategy development and fundraising prospectus. Leonard has MCP connections to Stratafy and Linear in Claude. Multi-workspace MCP access not yet available (enhancement logged) — will need separate API key for STIR workspace.

## Research
No research recorded

## Decision
Use Stratafy for strategic execution (foundation, strategy, alignment, insights, decisions), Linear for operational execution (tasks, projects, sprints, team coordination), and Claude with MCP connections to both as the intelligence layer that bridges strategic intent and operational action.

## Rationale
This mirrors the AI Operations Stack pattern documented in Category Creation strategy: Strategic Context (Stratafy) → Coordination (Linear) → Intelligence (Claude/MCP). Using this stack for STIR validates the pattern externally for the first time. It also keeps strategic and operational concerns cleanly separated while connected — strategy lives in Stratafy, execution lives in Linear, and Claude can reason across both with full context. This is the exact architecture we're selling.

## Outcome
No outcome recorded yet
