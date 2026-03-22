---
id: b3790ca6-f4b9-42ff-abb0-d4529028f23b
type: initiative
status: active
priority: critical
strategy: Strategic Intelligence
completionPercentage: 0
---

# Daily Rhythm — Role-Aware Check-ins & Operational Sensing

## Description
The daily operational capture layer for Stratafy. Morning (/lets-go) and evening (/call-it-a-day) commands in the team plugin provide role-aware check-ins for advisors, CEOs, and team members. Stores structured data in check_in_sessions and check_in_items tables — wins, blockers, learnings, observations, priorities — linked to strategies, initiatives, and objectives. Feeds the CEO Daily Digest and provides the raw data layer that Pulse's weekly alignment engine reads from. Ships through the team plugin; no separate product surface needed.

## Parent Strategy
[Strategic Intelligence](../strategy/product/strategic-intelligence.md)

## Status & Progress
- **Status**: active
- **Priority**: critical
- **Completion**: 0%

## Key Objectives
No objectives defined

## Timeline
- **Start Date**: 2026-02-11
- **Target Date**: 2026-06-30

## Content
# Daily Rhythm — Role-Aware Check-ins & Operational Sensing

## Purpose

The daily rhythm is Stratafy's operational sensing layer. It captures what's actually happening — what people are working on, what's blocked, what they learned, what they noticed — and turns it into structured data that feeds morning briefings, the CEO digest, and eventually Pulse's weekly alignment scoring.

This is distinct from Pulse. Pulse monitors alignment drift over time through weekly reflective conversations. The daily rhythm captures operational reality in the moment. Daily feeds weekly; they're complementary, not competing.

---

## Components

### Team Plugin Commands

**`/lets-go`** — Morning check-in
- Pulls strategic context (active strategies, key priorities, recent signals)
- Shows what teammates reported yesterday (from their evening check-ins)
- Asks what the person is working on today
- Links committed work to strategies/initiatives where possible
- Role-aware presentation (see below)

**`/call-it-a-day`** — Evening wrap
- Conversational reflection: what happened, what's blocked, what did you learn?
- Captures structured items (wins, blockers, learnings, observations, concerns, priorities)
- Links items to strategic entities where relevant
- Creates a check-in session record with summary
- Detects recurring themes via content hashing

**`/coach-me`** — Socratic coaching grounded in workspace context
**`/advise-me`** — Direct strategic recommendations personalised to role

### CEO Daily Digest
- Aggregates previous day's check-in data across the workspace
- Check-in rates, productivity sentiment, alignment indicators
- Blockers surfaced across teams (with recurrence counts)
- Insights captured during evening reflections
- Delivered via existing messaging channels (WhatsApp, Google Chat)

---

## Role-Aware Architecture

The same team plugin adapts behaviour based on the user's role in the workspace:

### Advisor (e.g. Rich at Missing Link)

**Morning (`/lets-go`):**
- CoS-style briefing: "Here's what's happening in the business"
- Yesterday's check-in highlights from CEO and team
- Key risks, pending decisions, unprocessed signals
- Suggested focus areas for advisory input
- Then transitions to: "What would you like to work on?"

**Evening (`/call-it-a-day`):**
- Captures observations and strategic recommendations
- Items tagged as `advisor_observation` for special weighting
- Prompts for any concerns or pattern recognition

### CEO

**Morning (`/lets-go`):**
- Operational briefing: team check-in summary, blockers, priorities
- Strategy health snapshot (Pulse-lite from existing data)
- Decisions waiting, risks escalated
- "Here's what your team committed to yesterday. Here's what needs your attention."

**Evening (`/call-it-a-day`):**
- Captures wins, blockers, decisions made, learnings
- Prompts: "Anything your team should know tomorrow?"
- Tomorrow's priority setting

### Team Member

**Morning (`/lets-go`):**
- Strategic context: "Here's why your work matters" — connects daily tasks to strategy
- What the CEO/advisor flagged yesterday (filtered to relevance)
- "What are you working on today?"

**Evening (`/call-it-a-day`):**
- What did you get done? What's stuck? What did you learn?
- Lightweight, conversational, 2-3 minutes max

---

## Early-Stage Mode

For new workspaces without defined strategies, metrics, or objectives (like Missing Link at onboarding):

- Victory condition anchoring instead of strategy alignment: "What does winning look like this week?"
- Conversational task gathering instead of pulling from project management tools
- Items captured still get stored in check-in tables for future linking
- As strategy gets defined, the daily rhythm automatically becomes richer

Detection: workspace has no active strategies OR only draft strategies with no objectives.

---

## Database Schema

### `check_in_sessions` — The conversation wrapper

| Field | Type | Description |
|---|---|---|
| id | uuid | Primary key |
| workspace_id | uuid | FK to workspaces |
| user_id | uuid | FK to users |
| user_name | text | Denormalised for quick display |
| user_role | enum | advisor, ceo, team, coach |
| session_type | enum | lets_go, call_it_a_day |
| session_date | date | The calendar date this check-in covers |
| summary | text | AI-generated summary of the conversation |
| sentiment | enum | positive, neutral, mixed, negative |
| alignment_score | smallint | Optional 0-100 alignment indicator |
| paired_session_id | uuid | Links morning ↔ evening sessions |
| briefing_given | jsonb | Snapshot of what was presented in morning briefing |
| committed_work | jsonb | What the person said they'd work on (morning) |
| tomorrow_priority | text | What they flagged for tomorrow (evening) |
| followed_through | boolean | Did evening items match morning commitments? |
| tags | text[] | Flexible tagging |
| created_at | timestamptz | |
| updated_at | timestamptz | |

**Indexes:** workspace_id + session_date, user_id + session_date, paired_session_id

### `check_in_items` — Individual things captured

| Field | Type | Description |
|---|---|---|
| id | uuid | Primary key |
| session_id | uuid | FK to check_in_sessions |
| workspace_id | uuid | FK to workspaces (denormalised for fast queries) |
| item_type | enum | win, blocker, learning, observation, concern, priority |
| content | text | What the person said |
| context | text | Additional context or AI-inferred detail |
| strategy_id | uuid | Optional FK — linked strategy |
| initiative_id | uuid | Optional FK — linked initiative |
| objective_id | uuid | Optional FK — linked objective |
| insight_id | uuid | Optional FK — promoted to insight |
| signal_id | uuid | Optional FK — promoted to signal |
| risk_id | uuid | Optional FK — promoted to risk |
| content_hash | text | Hash for recurring theme detection |
| recurrence_count | integer | How many times this theme has appeared |
| first_seen_at | timestamptz | When this theme first appeared |
| position | smallint | Order within the session |
| tags | text[] | Flexible tagging |
| created_at | timestamptz | |
| updated_at | timestamptz | |

**Indexes:** session_id, workspace_id + item_type, content_hash, strategy_id, initiative_id

---

## Data Flow

```
Evening check-in (write)
    → check_in_sessions + check_in_items
    → recurring themes detected via content_hash
    → items promoted to insights/signals/risks when warranted
    ↓
Morning briefing (read)
    → pulls yesterday's check-ins for relevant roles
    → combines with strategy health data (Pulse-lite)
    → presents role-appropriate briefing
    ↓
CEO Daily Digest (aggregate)
    → all check-in data for previous day
    → check-in rates, sentiment distribution, blocker count
    → delivered via messaging channel
    ↓
Pulse Weekly (aggregate + assess)
    → reads week's check-in items as input signal
    → runs its own adaptive alignment conversation
    → computes Understanding, Initiative Alignment, Purpose Connection scores
    → stores in pulse_sessions / pulse_scores (separate tables)
```

---

## Relationship to Other Features

| Feature | Relationship |
|---|---|
| **Pulse (Weekly)** | Daily rhythm feeds Pulse. Check-in items are input signals for Pulse's alignment assessment. Separate tables, connected by the Pulse engine reading from check-in data. |
| **CEO Daily Digest** | Downstream consumer. Aggregates check-in data into executive summary. |
| **Insights** | Check-in items can be promoted to insights when they represent strategic learnings. |
| **Signals** | Observations from check-ins can become signals when they indicate external/internal change. |
| **Risks** | Recurring blockers can be promoted to risks when they represent systemic threats. |
| **Radar** | Radar senses externally; daily rhythm senses internally. Both feed Cortex. |

---

## Implementation Phases

### Phase 1: Plugin Commands (Done)
- /lets-go and /call-it-a-day exist in team plugin
- Role-aware presentation templates designed
- Early-stage mode specified
- ~~Linear integration~~ removed — conversational task gathering instead

### Phase 2: Database Tables (Next)
- Create check_in_sessions and check_in_items tables
- MCP tools: create_check_in_session, add_check_in_item, list_check_ins, get_check_in_summary
- Update plugin commands to write to tables instead of creating ad-hoc insights
- Content hash computation for recurring theme detection

### Phase 3: CEO Daily Digest
- Aggregation queries across workspace check-ins
- Template for digest output
- Messaging channel delivery (WhatsApp/Google Chat integration)
- Timeline: after 2+ weeks of check-in data

### Phase 4: Pulse Integration
- Pulse weekly engine reads from check_in_items as input signal
- Check-in completion rates feed into Pulse health scoring
- Recurring themes surface in Pulse's adaptive questioning

---

## Success Metrics
- Daily check-in completion rate (% of active users)
- Session pair completeness (% of mornings with matching evenings)
- Items captured per session (target: 3-5 per evening)
- Theme promotion rate (% of items that become insights/signals/risks)
- Follow-through rate (evening items matching morning commitments)
- CEO digest engagement rate
- Time from blocker surfaced to resolution
