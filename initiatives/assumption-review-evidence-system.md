---
id: 61a021a4-570b-40f8-bcd2-f63a06e58d95
type: initiative
status: in_progress
priority: high
strategy: Strategic Intelligence
completionPercentage: 90
---

# Assumption Review & Evidence System

## Description
Evidence capture and research system for strategic assumptions. Three capabilities: (1) review_assumptions — surfaces assumptions by urgency: overdue deadlines, critical-impact hypotheses untested, stale evidence, linked strategy health changes. No AI scoring — prioritised surfacing for human judgment. (2) research_assumption — takes an assumption, generates targeted web search queries, fetches and synthesises findings into structured evidence with direction (supports/contradicts/neutral). External/market assumptions that can't be tested from workspace data. (3) log_assumption_evidence — low-friction capture when humans have evidence from conversations, observations, or discoveries. New assumption_evidence table provides structured evidence trail per assumption (replacing the single validation_evidence text field for accumulation). Confidence updates remain human-decided via existing enum (hypothesis/likely/validated/invalidated) — no automated numeric scoring. Delivered via MCP tools consumed by CSIO/CTO plugin commands. ~10 hours build.

## Parent Strategy
[Strategic Intelligence](../strategy/product/strategic-intelligence.md)

## Status & Progress
- **Status**: in progress
- **Priority**: high
- **Completion**: 90%

## Key Objectives
- [At least 2 assumption confidence levels updated based on gathered evidence](../objectives/at-least-2-assumption-confidence-levels-updated-based-on-gathered-evidence.md)
- [100% of critical-impact assumptions have at least one evidence entry](../objectives/100-of-critical-impact-assumptions-have-at-least-one-evidence-entry.md)
- [External research tool validated against 3 Stratafy assumptions with actionable findings](../objectives/external-research-tool-validated-against-3-stratafy-assumptions-with-actionable-.md)
- [All three MCP tools live — review, research, and log_evidence](../objectives/all-three-mcp-tools-live-review-research-and-log-evidence.md)
- [assumption_evidence table live with RLS and service layer](../objectives/assumption-evidence-table-live-with-rls-and-service-layer.md)

## Timeline
- **Start Date**: 2026-03-24
- **Target Date**: 2026-04-07

## Content
# Assumption Review & Evidence System

## The Problem

Assumptions are the hidden load-bearing walls of strategy. Stratafy already tracks 31 assumptions with confidence levels, impact ratings, validation methods, and strategy links. What's missing: **nobody goes back to check them.** Validation deadlines pass silently. Evidence appears (a prospect conversation, a market signal, a competitor move) but never gets connected to the assumption it validates or invalidates.

The original "Assumption Intelligence Engine" spec proposed automated AI scoring (0-100) against internal workspace data. Analysis showed this is premature:
- Most critical assumptions (market, strategic) aren't testable from workspace data — they need external research or human evidence
- With 1 paying customer and sparse metrics, AI scoring produces false precision
- 31 assumptions don't need batch processing — a human can review them in 20 minutes
- The automated scoring engine becomes valuable at scale (100+ assumptions, rich metric history) — that's Phase 2

## What We're Building Instead

A **review and evidence system** that makes the human process work, generates the data that makes future automation accurate, and adds AI-powered external research for market/strategic assumptions.

---

## Three MCP Tools

### 1. `review_assumptions`
**Purpose:** Surface what needs attention — the forcing function.

Ranks assumptions by urgency:
- Past validation deadlines (parsed from validation_evidence text)
- Critical/high impact still at hypothesis confidence
- No evidence logged in 30+ days (stale)
- Assumptions where linked strategy health has changed since last evidence

Returns a prioritised list with context: assumption statement, linked strategies, impact, current confidence, last evidence date, why it's surfaced.

**No AI scoring.** Just prioritised surfacing for human judgment.

### 2. `research_assumption`
**Purpose:** AI-powered external evidence gathering for market/strategic assumptions.

Flow:
1. Read assumption statement, type, and validation_method
2. Generate 3-5 targeted search queries from the assumption
3. Use `fetch_content` to research across web sources
4. Synthesise findings into structured evidence:
   - Direction: supports / contradicts / neutral
   - Summary: 2-3 sentence synthesis
   - Sources: URLs with relevance notes
   - Confidence assessment: what the evidence suggests
5. Write an `assumption_evidence` row
6. Return findings to the user — human decides whether to update confidence

**This is the core new capability.** Assumptions like "VCs will pay a premium for strategy-specific AI infrastructure" or "MCP achieves broad ecosystem adoption" can be actively researched rather than waiting for signal.

### 3. `log_assumption_evidence`
**Purpose:** Low-friction evidence capture from human observations.

After a prospect conversation, a customer call, a demo reaction — one command to log what was learned:
- Which assumption(s) it relates to
- What the evidence is
- Direction: supports / contradicts / neutral
- Source: conversation, observation, metric, signal

Used by any plugin during natural workflow. CSIO can also suggest connections: "This signal may be evidence for assumption X."

---

## Data Model

### New table: `assumption_evidence`

```sql
CREATE TABLE assumption_evidence (
  id uuid PRIMARY KEY DEFAULT gen_random_uuid(),
  assumption_id uuid NOT NULL REFERENCES assumptions(id) ON DELETE CASCADE,
  workspace_id uuid NOT NULL REFERENCES ws_workspaces(id) ON DELETE CASCADE,
  
  evidence_type text NOT NULL DEFAULT 'observation',  -- 'research' | 'observation' | 'metric' | 'signal'
  direction text NOT NULL DEFAULT 'neutral',           -- 'supports' | 'contradicts' | 'neutral'
  
  summary text NOT NULL,                               -- What was found
  sources jsonb DEFAULT '[]',                          -- URLs, entity refs, search queries
  
  confidence_snapshot text,                            -- Confidence at time of logging
  
  created_at timestamptz NOT NULL DEFAULT now(),
  created_by uuid NOT NULL REFERENCES ws_users(id)
);
```

This is the structured evidence log. Each row is one piece of evidence. The existing `validation_evidence` text field on assumptions stays for the final verdict summary; this table captures the accumulating journey.

RLS: workspace-scoped, same pattern as other strategy entities.

### No other schema changes needed
- `confidence` enum stays as-is (hypothesis/likely/validated/invalidated) — human-decided
- No numeric scoring field
- No confidence_history table — evidence rows ARE the history

---

## Service Layer

### `AssumptionEvidenceService` (new)
- `logEvidence(assumptionId, data)` — write evidence row
- `listEvidence(assumptionId)` — get evidence trail for an assumption
- `getEvidenceSummary(workspaceId)` — aggregate stats: assumptions with evidence, without, stale

### `AssumptionReviewService` (new)
- `reviewAssumptions(workspaceId)` — the urgency ranking logic
- `researchAssumption(assumptionId)` — query generation, web fetch, synthesis, evidence logging

---

## Plugin Integration

### CSIO `/assumption-review` command
Calls `review_assumptions`, walks through the critical ones, prompts for action on each:
- Research it (calls `research_assumption`)
- Log evidence from a conversation
- Update confidence
- Dismiss for now

### Any plugin — post-signal evidence capture
After logging a signal or insight, plugins can suggest: "This may be evidence for assumption X — want to log it?" Uses semantic search to find relevant assumptions.

---

## What's NOT in scope

- **No numeric 0-100 scoring** — enum confidence levels + human judgment
- **No background cron** — plugin-triggered review
- **No dashboard UI** — conversational delivery first
- **No internal workspace data scanning** — deferred until metric density justifies it
- **No auto-classification** — assumption_type already exists
- **No Radar integration** — standalone research capability for now

---

## Phasing

### Phase 1 (This build — ~10 hours)
- `assumption_evidence` table + RLS + service
- `review_assumptions` MCP tool (urgency surfacing)
- `log_assumption_evidence` MCP tool (manual capture)
- `research_assumption` MCP tool (web research + synthesis)
- CSIO plugin command wiring

### Phase 2 (When workspace data is rich — post-PMF)
- Internal evidence path: test assumptions against metrics, initiative progress, check-in data
- Automated weekly review cycle (background job)
- Confidence trend tracking and threshold alerts
- Strategy review trigger when evidence accumulates against an assumption

### Phase 3 (At scale — 50+ workspaces)
- Numeric confidence scoring (0-100) from combined evidence
- Assumption dashboard UI
- Cross-workspace benchmarking
- Weekly digest in check-in flow

---

## Why This Matters Now

1. **5 critical-impact hypotheses have validation deadlines this week** (March 28, March 31). The review tool surfaces these immediately.
2. **External assumptions are researchable today.** "VCs will pay for strategy-specific infrastructure" — AI can research this now, not wait for customer data.
3. **Evidence compounds.** Every research run and observation logged makes Phase 2 automated scoring more accurate.
4. **Demo differentiator.** "Our platform doesn't let your strategy run on untested premises" — honest, differentiated, achievable.
5. **Dog-food value.** Run it on Stratafy's own 31 assumptions to validate the feature AND answer real strategic questions.

---

## Success Criteria

- All critical-impact assumptions have at least one evidence entry within 2 weeks
- External research produces actionable findings (not generic summaries)
- Evidence capture is low enough friction that it happens naturally during plugin sessions
- At least 2 assumption confidence levels updated based on gathered evidence
