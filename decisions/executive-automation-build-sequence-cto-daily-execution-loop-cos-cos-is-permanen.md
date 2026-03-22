---
id: 8d100338-d0f4-4a23-ac4b-70a85dc2eb49
type: decision
decisionType: type_1_irreversible
status: decided
decidedAt: 2026-03-15T10:51:24.17+00:00
---

# Executive automation build sequence: CTO → Daily Execution Loop → CoS; CoS is permanently read-only

## Description
Two related decisions captured together. First: the correct build sequence for the executive automation pattern, driven by three risks — context window pressure under full /brief load before the Hot Strategic Context Cache is built, write authority ambiguity if the CoS can surface suggestions that look like decisions in the same session, and stale data if /brief runs against an unrefreshed workspace. Second: the CoS must be explicitly read-only — it orchestrates and synthesises but never mutates. Write authority stays with individual executive plugins, scoped to their owned strategies.

## Details
- **Type**: Type 1 (Irreversible)
- **Status**: decided
- **Authority**: Leonard Cremer (Founder & CEO)
- **Deadline**: No deadline
- **Decided At**: 2026-03-15T10:51:24.17+00:00

## Context
No context recorded

## Research
No research recorded

## Decision
Build sequence: (1) CTO plugin + /engage — validates single-executive activation pattern; (2) Daily Execution Loop — ensures workspace freshness before CoS has anything useful to read; (3) CoS + /brief — orchestration layer, built on fresh data and a proven single-executive pattern; (4) True parallel execution via Anthropic API — post-seed. CoS is read-only at all times — it can surface and recommend but cannot propose workspace mutations. Only individual executive plugins can write, and only within their owned strategies.

## Rationale
Building CoS before CTO plugin and Daily Execution Loop creates three failure modes: context window overflow before synthesis step, CoS surfacing stale intelligence confidently, and ambiguous write authority in a consolidated session. Sequencing resolves all three. The read-only constraint on CoS is a governance boundary — the CoS sees everything but owns nothing, which is architecturally consistent with how a real Chief of Staff operates.

## Outcome
No outcome recorded yet
