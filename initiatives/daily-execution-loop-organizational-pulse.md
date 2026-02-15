---
id: b3790ca6-f4b9-42ff-abb0-d4529028f23b
type: initiative
status: active
priority: critical
strategy: Strategic Intelligence
completionPercentage: 0
lastUpdated: 2026-02-13T07:06:41.446+00:00
owner: af04d126-d28a-43a7-be8b-0c9451873f1b
---

# Daily Execution Loop & Organizational Pulse

## Description
Build the daily execution loop through /Let's go and /Call it a day MCP prompts (already implemented), plus dual-layer session logging infrastructure. Layer 1: MCP server logs prompt selection events (reliable check-in tracking). Layer 2: Prompt templates instruct Claude to create insights during sessions (rich content capture). Together they enable the CEO Daily Digest — organizational pulse data from individual execution sessions. Three logging events: session start (/Let's go), session end (/Call it a day), and insights captured during end-of-day reflection. Phase 1 (prompt-embedded logging) can ship immediately with no backend changes. Phase 2 (server-side logging) requires MCP server update.

## Parent Strategy
[Strategic Intelligence](../strategy/functional/strategic-intelligence.md)

## Status & Progress
- **Status**: active
- **Priority**: critical
- **Completion**: 0%

## Key Objectives
- [20+ daily execution sessions logged before Pieter meeting](../objectives/20-daily-execution-sessions-logged-before-pieter-meeting.md)

## Timeline
- **Start Date**: 2026-02-11
- **Target Date**: 2026-02-16

## Content
## Components

### MCP Prompts (Individual Level)
1. **/Coach me** — Role-aware Socratic coaching grounded in workspace context
2. **/Advise me** — Direct strategic recommendations personalized to user role and context
3. **/Let's go** — Pulls Linear tasks, cross-references with strategy, helps user execute
4. **/Call it a day** — End-of-day reflection capturing productivity sentiment, alignment, blockers, insights

### CEO Daily Digest (Executive Level)
- Check-in rates across the organization
- Aggregate productivity sentiment
- Strategic alignment scores
- Blockers surfaced across teams
- Insights captured during the day

## The Loop
Morning: /Let's go → execute with context
During day: /Coach me or /Advise me → guidance when stuck
End of day: /Call it a day → reflect, capture, close
Next morning: CEO digest → organizational pulse without meetings

## Logging Architecture (Dual Layer)

### Layer 1: MCP Server-Side Logging (Option C)
When a user selects a prompt via `prompts/get`, the MCP server logs the event before the conversation begins. This captures:
- **Prompt triggered** (which prompt: lets_go, call_it_a_day, coach_me, advise_me)
- **User ID** and **workspace ID**
- **Timestamp** of prompt selection
- **Session type** derived from prompt (morning_start, end_of_day, coaching, advising)

This is the most reliable signal — it fires regardless of what happens in the conversation. Gives us check-in rates and timing data even if the user abandons the session.

### Layer 2: Prompt-Embedded Insight Logging (Option B)
The prompt templates themselves instruct Claude to call Stratafy tools during the conversation:

**On /Let's go:**
- Prompt instructs Claude to call `create_insight` with `source: "execution_session"` and tag `session_start` at the beginning of the interaction
- Captures: date, time, user context

**On /Call it a day:**
- Prompt instructs Claude to call `create_insight` with `source: "execution_session"` and tag `session_end` at the beginning of the interaction
- **During the reflection**, as insights emerge from the conversation, Claude calls `create_insight` for each with `source: "execution_session"` and relevant category/tags
- This creates a stream of insights tied to the daily reflection, not just a single log entry

### Why Both Layers

| Signal | Layer 1 (Server) | Layer 2 (Prompt) |
|--------|------------------|------------------|
| User started a session | ✅ Reliable | ✅ But could fail if user cancels early |
| Session duration | ✅ Can correlate with end event | ❌ No direct measurement |
| Check-in rates | ✅ Most accurate | ⚠️ Partial — only if insight fires |
| Insights from reflection | ❌ No content access | ✅ Rich, contextual insights |
| Blockers surfaced | ❌ | ✅ Captured via insight pipeline |
| Strategic alignment data | ❌ | ✅ Captured during /Call it a day |
| Works if conversation fails | ✅ | ❌ |

Together they give complete coverage: server-side for reliable events, prompt-side for rich content.

## What Gets Logged

### Event 1: Session Start (/Let's go)
- Server log: prompt_id, user_id, workspace_id, timestamp, session_type: morning_start
- Insight: name="Session Start", source="execution_session", tags=["session_start", date]

### Event 2: Session End (/Call it a day)
- Server log: prompt_id, user_id, workspace_id, timestamp, session_type: end_of_day
- Insight: name="Session End", source="execution_session", tags=["session_end", date]

### Event 3: Insights During Reflection
- As user reflects during /Call it a day, Claude captures insights naturally
- Each insight logged via `create_insight` with source="execution_session"
- Categories assigned based on content (strategic, operational, product, etc.)
- These flow into the existing insight pipeline for synthesis and review

## Dependencies
- MCP server enhancement to log `prompts/get` events (Layer 1)
- Prompt template updates to include logging instructions (Layer 2)
- Existing `create_insight` MCP tool (already built)
- Linear MCP integration for /Let's go task pulling
- Role-aware context packaging for personalized coaching
- Aggregation queries for CEO digest

## Implementation Phases

### Phase 1: Prompt-Embedded Logging (Ship first — no backend changes)
- Update /Let's go prompt template: add instruction to create session_start insight
- Update /Call it a day prompt template: add instruction to create session_end insight + capture insights during reflection
- Test with Leonard's own daily usage
- Timeline: Can ship immediately

### Phase 2: MCP Server-Side Logging
- Add logging hook to `prompts/get` handler in MCP server
- Log to existing MCP activity table or new prompt_events table
- Capture: prompt_id, user_id, workspace_id, timestamp
- Timeline: Next MCP deployment

### Phase 3: CEO Daily Digest
- Aggregate session events across workspace users
- Check-in rates, timing patterns, insight volume
- Blockers surfaced, strategic themes
- Timeline: After STIR has 2+ weeks of data

## Success Metrics
- Daily active prompt usage per user
- Check-in completion rate (start + end pairs)
- Insight capture rate from /Call it a day sessions
- Blocker-to-resolution time
- CEO digest engagement rate
- Strategy update rate from aggregated feedback
- Session pair completeness (% of /Let's go that have matching /Call it a day)
