---
id: f817d84d-acd4-42bb-bf42-442f682ab5ee
type: initiative
status: draft
priority: medium
strategy: Strategic Intelligence
completionPercentage: 0
---

# Internal Sensing (Pulse) — Weekly Alignment Monitoring

## Description
Pulse's weekly alignment engine: adaptive Friday AI conversations (3-5 min) that measure Understanding, Initiative Alignment, and Purpose Connection. Reads from daily check-in data (check_in_items) as input signal, runs its own reflective conversation, and produces alignment scores with trend tracking, drift detection, and early warning alerts. Stores in pulse_sessions, pulse_scores, pulse_trends, and pulse_alerts tables — separate from the daily rhythm's check_in tables. The partner residency tool for firms like We Are 52, turning project-based engagements into retainer-based monitoring.

## Parent Strategy
[Strategic Intelligence](../strategy/product/strategic-intelligence.md)

## Status & Progress
- **Status**: draft
- **Priority**: medium
- **Completion**: 0%

## Key Objectives
No objectives defined

## Timeline
- **Start Date**: 2026-07-01
- **Target Date**: 2026-09-30

## Content
## Overview

Internal Sensing via Pulse is Stratafy's weekly alignment monitoring engine — the "heartbeat" of a strategic engagement. It runs asynchronous, individual, recurring check-ins (3-5 minute Friday AI conversations) and turns responses into alignment trend data, early warning signals, and drift detection.

Pulse is a **monitoring tool** — not a facilitation tool. That's InsightSync. Pulse watches; InsightSync convenes.

---

## Relationship to Daily Rhythm

The Daily Rhythm initiative (check-in sessions and items) captures **operational reality** — what people are working on, what's blocked, what they learned. It runs daily through `/lets-go` and `/call-it-a-day`.

Pulse is different. It measures **alignment** — do people understand the strategy, is their work connected to it, do they find personal meaning in it? It runs weekly through a dedicated reflective conversation.

**How they connect:**
- Pulse reads from `check_in_items` as an input signal when preparing its Friday questions
- If daily check-ins show recurring blockers against an initiative, Pulse probes deeper on that
- If wins are clustering around one strategy and silence around another, Pulse detects drift
- Daily rhythm stores in `check_in_sessions` / `check_in_items`; Pulse stores in its own tables
- Separate storage, connected intelligence

---

## The Four Layers

### 1. Weekly AI Check-ins
- Brief Friday conversations with team members (3-5 minutes)
- AI-powered dialogue focused on strategic understanding and alignment
- Adaptive questioning based on previous responses, trends, AND daily check-in data from that week
- Should feel like a brief reflection, not a survey

### 2. Dynamic Trend Tracking
- Week-over-week alignment measurement across three components:
  - **Understanding** — comprehension of strategic direction
  - **Initiative Alignment** — connection between daily work and strategic initiatives
  - **Purpose Connection** — personal meaning and motivation
- Statistical trend analysis and pattern recognition
- Confidence intervals and reliability scoring

### 3. Early Warning System
- Automatic identification of strategic drift indicators
- Threshold alerts when alignment degrades below critical levels
- Predictive modelling for potential execution problems
- Escalation protocols for leadership or partner intervention

### 4. Adaptive Guidance
- AI-generated recommendations for reinforcing weakening alignment areas
- Personalised suggestions based on individual and team patterns
- Success pattern recognition and best practice sharing

---

## Database Schema

### `pulse_sessions` — The weekly conversation wrapper

| Field | Type | Description |
|---|---|---|
| id | uuid | Primary key |
| workspace_id | uuid | FK to workspaces |
| user_id | uuid | FK to users |
| session_date | date | The Friday this pulse covers |
| session_week | integer | ISO week number for trend grouping |
| understanding_score | smallint | 0-100 comprehension score |
| initiative_alignment_score | smallint | 0-100 work-connection score |
| purpose_connection_score | smallint | 0-100 personal meaning score |
| composite_alignment_score | smallint | Weighted composite of three components |
| previous_session_id | uuid | FK to previous pulse for delta calculation |
| check_in_items_considered | integer | How many daily check-in items were read as input |
| summary | text | AI-generated summary of the reflection |
| created_at | timestamptz | |

### `pulse_responses` — Individual question-answer pairs

| Field | Type | Description |
|---|---|---|
| id | uuid | Primary key |
| session_id | uuid | FK to pulse_sessions |
| question | text | The adaptive question asked |
| response | text | The person's answer |
| component | enum | understanding, initiative_alignment, purpose_connection |
| score_contribution | smallint | How this response contributed to the component score |
| position | smallint | Order in conversation |

### `pulse_trends` — Aggregated trend data

| Field | Type | Description |
|---|---|---|
| id | uuid | Primary key |
| workspace_id | uuid | FK to workspaces |
| user_id | uuid | Null for team-level trends |
| team_id | uuid | Null for individual trends |
| week_number | integer | ISO week |
| understanding_avg | numeric | Average understanding score |
| initiative_alignment_avg | numeric | Average initiative alignment |
| purpose_connection_avg | numeric | Average purpose connection |
| composite_avg | numeric | Weighted composite |
| delta_from_previous | numeric | Week-over-week change |
| sample_size | integer | Number of pulse sessions in this aggregate |

### `pulse_alerts` — Threshold breaches and drift warnings

| Field | Type | Description |
|---|---|---|
| id | uuid | Primary key |
| workspace_id | uuid | FK to workspaces |
| alert_type | enum | drift, threshold_breach, trend_reversal, low_participation |
| severity | enum | info, warning, critical |
| component | enum | understanding, initiative_alignment, purpose_connection, composite |
| message | text | Human-readable alert |
| context | jsonb | Supporting data |
| acknowledged_at | timestamptz | When someone acted on it |
| created_at | timestamptz | |

---

## Partner Application (We Are 52)

Pulse is the **monitoring layer** of the partner engagement model:

- **Client residency:** Keeps partners embedded between milestone sessions through live data feed
- **Proof of impact:** "Alignment on Talent Engine improved from 42% to 67% over 8 weeks" — concrete ROI
- **Commercial model:** Changes from project-based to retainer-based engagement
- **Adaptive questioning:** Grounded in partner's diagnostic outputs (e.g. We Are 52's four people pillars)

---

## Implementation Timeline
- Phase 3 in Product Architecture roadmap (Q3 2026)
- Depends on: Daily Rhythm tables shipping first (provides input data)
- Start date: 2026-07-01 | Target: 2026-09-30

## Expected Outcomes
- Execution drift detected weeks earlier through automated monitoring
- Weekly visibility into alignment trends across three components
- Partners maintain continuous client residency between sessions
- Data-driven proof of impact for partner commercial model
- Complete internal sensing loop: daily operational capture → weekly alignment assessment → trend tracking → early warning
