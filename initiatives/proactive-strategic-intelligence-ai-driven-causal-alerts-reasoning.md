---
id: 5fbc9f19-99a8-4688-9fa2-7ffd9e04c070
type: initiative
status: in_progress
priority: critical
strategy: Strategic Intelligence
completionPercentage: 70
---

# Proactive Strategic Intelligence — AI-Driven Causal Alerts & Reasoning

## Description
Stratafy automatically detects when external signals, internal execution, or silent drift change the validity of your strategy, explains the causal impact in clear plain language, and presents a simple decision prompt — so users stay aligned with minimal effort and maximum trust. The system fires on both event-driven triggers (new Radar findings, Insights, metric shifts, assumption confidence changes) and time-based triggers (evidence aging, provenance staleness, elements with no recent review). The user never searches for intelligence — it comes to them. Every alert is one sentence of impact plus one clear action. If the system has nothing important to say, it says nothing.

## Parent Strategy
[Strategic Intelligence](../strategy/product/strategic-intelligence.md)

## Status & Progress
- **Status**: in progress
- **Priority**: critical
- **Completion**: 70%

## Key Objectives
- [Silent drift detected before it causes visible damage](../objectives/silent-drift-detected-before-it-causes-visible-damage.md)
- [The system surfaces strategic issues users would have missed](../objectives/the-system-surfaces-strategic-issues-users-would-have-missed.md)
- [Users trust and act on the surfaced intelligence](../objectives/users-trust-and-act-on-the-surfaced-intelligence.md)
- [Users receive timely, actionable intelligence without manual monitoring](../objectives/users-receive-timely-actionable-intelligence-without-manual-monitoring.md)
- [Successful validation in real customer environment](../objectives/successful-validation-in-real-customer-environment.md)
- [Clear proof of the consumption = maintenance flywheel](../objectives/clear-proof-of-the-consumption-maintenance-flywheel.md)
- [Reduction in manual strategic alignment effort](../objectives/reduction-in-manual-strategic-alignment-effort.md)
- [High user trust and perceived value](../objectives/high-user-trust-and-perceived-value.md)

## Timeline
- **Start Date**: 2026-03-31
- **Target Date**: 2026-04-15

## Content
## What the User Actually Experiences

You open Stratafy (or your Advisor briefing) on a normal morning and see something like this:

> **Advisor:** "One of your key assumptions weakened over the weekend.
> A new Radar finding about coaches using general-purpose AI tools challenges Assumption A-14 (Coach Network adoption).
> **Impact:** This puts pressure on our primary GTM strategy and 4 linked initiatives (including STIR Collective).
> Would you like to review the details, adjust confidence, or take action?"

Or this:

> **Advisor:** "Your strategy has experienced silent drift over the past 19 days.
> The provenance supporting Assumption A-9 ('Coach Network GTM will be our primary distribution channel') has gradually weakened. 71% of the evidence was created before the recent surge in coaches using general-purpose Claude Projects.
> **Impact:** This is reducing confidence in our Coach Network and Advisory Firms strategies and is now affecting STIR Collective progress.
> Would you like to review the full lineage, refresh the evidence, adjust the assumption, or take no action for now?"

You reply with a simple "yes", "explain more", "update confidence to Hypothesis", or "refresh evidence".
That's it. The user's job is **to respond to intelligence**, not to monitor, review dashboards, or hunt for connections.

## What Simple Looks Like

- The user never searches for intelligence — it comes to them.
- Every alert is one sentence of impact + one clear action.
- If the system has nothing important to say, it says nothing.

## Objective

Build a system where Stratafy automatically detects when external signals, internal execution, or silent provenance drift change the validity of your strategy, explains the causal impact in clear, plain language, and presents you with a simple decision prompt — so you can stay aligned with minimal effort and maximum trust.

## Two Trigger Types, One System

### Event-Driven Triggers (something new happened)
- Assumption confidence changes from new evidence
- High-impact Radar findings or Insights
- Metric movements that contradict assumptions
- Causal chains propagating across the strategy graph

### Time-Based Drift Triggers (nothing happened and that's the problem)
- Evidence aging: supporting evidence predates significant external changes
- Provenance staleness: important elements with no recent review or challenge
- Confidence decay: high-impact assumptions with stale evidence that hasn't been refreshed
- Gaps in provenance: strategic elements with weak or missing sourcing

Both trigger types produce the same output: a plain-language alert with causal reasoning and a simple decision prompt, delivered via the Advisor.

## Progress — What's Built and Deployed

### Phase 0: Foundation Lock ✅
Assumption Review & Evidence System verified at 100%. 39 assumptions tracked, 52 evidence entries, all 4 MCP tools working (review_assumptions, research_assumption, log_assumption_evidence, list_assumption_evidence).

### Phase 1: Event-Driven Causal Engine ✅
- CausalChainService: forward-propagation graph traversal (assumption → assumption_contexts → strategies → initiatives → objectives + risks via risk_contexts)
- Severity scoring: strategies×4 + risks×3 + initiatives×2 + objectives×1, labels: low/medium/high/critical
- Plain-language summary generation
- MCP tools: trace_causal_chain, detect_active_chains
- Validated against live workspace data — single assumption touching 2 strategies, 6 initiatives, 5 objectives, 3 risks
- Commits: e11994a02, 351fc0abb

### Phase 2: Alert Delivery ✅
- Strategic Advisor prompt calls detect_active_chains on startup, leads with critical findings
- Let's Go prompt adds Step 0 checking for active chains before task prioritization
- Both prompts list causal chain + assumption intelligence tools
- Assumption detail page at /ws/:id/assumptions/:id with 3 tabs:
  - **Alerts tab**: pending alerts with action buttons (lower confidence, research, dismiss, snooze 7 days) + resolved alert history
  - **Evidence tab**: chronological trail (supports/contradicts/neutral)
  - **Causal Impact tab**: tree view grouped by strategy showing affected initiatives, objectives, risks
- Commits: a2bbcc565, b50faf4cb, 64d938a06

### Persisted Alert System ✅
- assumption_alerts table with full lifecycle: pending → acted/dismissed/snoozed
- AssumptionAlertService: create, list, respond, fire alerts for workspace
- MCP tools: fire_assumption_alerts, list_pending_alerts, respond_to_alert
- Narratives stored once (no LLM cost on repeat views)
- Action tracking enables measuring the 65% user action rate KR
- First live alert created for "Methodology HQs" assumption (high severity, 3 contradicting evidence entries)

## What's Remaining

### Phase 2.5: Causal Chain Persistence (not started)

**Problem:** Causal chains are currently computed on-the-fly and discarded. This means:
- No stable IDs to reference from Strategic Actions (`linked_entity_type: 'causal_chain'`)
- No historical comparison ("did this assumption's blast radius grow?")
- `detectActiveChains` recomputes from scratch every call (expensive: multiple DB queries per assumption)
- Phase 3 drift detection can't compare current vs previous chain state

**Solution:** Persist computed chains as lightweight snapshots.

**Schema: `causal_chain_snapshots`**
- `id` — stable UUID for linking from actions, alerts, etc.
- `workspace_id` — workspace scope
- `assumption_id` — the trigger assumption
- `chain_data` — JSONB: full CausalChain object (trigger, affected_nodes, summary)
- `severity_score`, `severity_label` — denormalized for filtering/sorting
- `affected_count` — number of affected nodes
- `computed_at` — when this snapshot was generated
- `stale_at` — computed_at + TTL (e.g. 24h), signals when to recompute
- `superseded_by` — points to the newer snapshot (for history traversal)
- Standard audit fields + RLS

**Recompute triggers:**
- New contradicting evidence logged on the assumption
- Assumption confidence changes
- `stale_at` exceeded (daily cron)

**Cache behavior:**
- `detectActiveChains` returns cached snapshots if fresh, recomputes if stale
- `traceFromAssumption` always computes fresh but persists the result
- Old snapshots kept for historical comparison (soft-deleted when superseded)

**Integration with Strategic Actions:**
- Actions can link to `linked_entity_type: 'causal_chain'`, `linked_entity_id: snapshot.id`
- Phase 2 auto-generated actions (from detectActiveChains) get stable provenance
- `origin_type: 'causal_chain'`, `origin_ref: snapshot.id`

**Deliverables:**
1. `causal_chain_snapshots` table with RLS, indexes, CHECK constraints
2. Update CausalChainService to persist on compute and serve from cache
3. MCP tool: `get_causal_chain_snapshot` for retrieving persisted chains
4. Wire `log_assumption_evidence` to trigger recomputation when contradicting evidence lands

### Phase 3: Drift Detection Layer (not started)
- Evidence freshness scoring: flag assumptions where evidence predates significant external changes
- Provenance staleness: flag high-impact elements with no review in N days
- Confidence decay detection: assumptions that should have been challenged but weren't
- Simpler than Phase 1 — mostly time-based queries against evidence timestamps, no graph traversal needed
- Drift alerts use the same delivery pipeline and persisted alert system from Phase 2
- **Now cheaper:** drift detection can compare current vs previous chain snapshots instead of recomputing full graphs

### Phase 4: Dogfood, Measure & Refine (not started)
- Week 1: Track alert accuracy — are causal chains correct? Are drift detections genuine?
- Week 2: Track user action rate — do people act on alerts?
- Week 3: Kill criterion check — if <30% action rate across both trigger types, reassess
- Ongoing: Iterate on alert quality based on inline feedback

### Open Items
- Hook log_assumption_evidence to auto-fire alerts when contradicting evidence is logged
- Daily cron for drift-based alert creation + stale chain recomputation
- Wire action buttons to actual operations (lower confidence → update_assumption, research → research_assumption)

## Key Results (User-Centric)

### MVP Success (by 2026-04-15 for event-driven, 2026-04-22 for drift)
- Users receive their first high-value proactive alert within 48 hours of a meaningful signal appearing.
- Average time from external signal to user notification < 4 hours.
- Average time from detectable provenance drift to user alert < 6 hours.
- Users act on (or explicitly dismiss) 65%+ of surfaced alerts without needing additional investigation.
- In our own workspace + STIR Collective, the system surfaces at least 8-10 meaningful insights (causal + drift) that the founder/team would not have caught manually in the same period.
- Alert quality feedback score >= 4.5/5.

### v1 Success (by 2026-04-30)
- Zero users disable or mute alerts.
- Repeat engagement: 80%+ of users who receive an alert interact with the next one.
- +40% increase in strategic intelligence depth (validated/invalidated assumptions + causal links + refreshed provenance) in 4 weeks.

### Kill Criterion
If after 3 weeks of dogfooding, fewer than 30% of alerts lead to any user action (including explicit dismissal with rationale), we stop and reassess whether the detection is producing signal or noise.

## MVP Scope

**In Scope (shipped):**
- Causal chain detection triggered by assumption confidence changes and high-impact Radar/Insight entries
- Plain-language explanation + business impact summary
- Simple decision prompt ("Review / Adjust confidence / Refresh evidence / Ignore / Escalate")
- Delivery via Advisor (daily briefing + conversational chat) + assumption detail page
- Persisted alerts with full lifecycle tracking
- Action buttons: lower confidence, research, dismiss, snooze 7 days
- Alert history with action tracking

**In Scope (remaining):**
- Causal chain snapshot persistence with cache and historical comparison
- Silent drift detection based on provenance aging, evidence quality decay, and review staleness
- Auto-fire alerts on evidence logging
- Daily cron for drift detection + stale chain recomputation

**Out of Scope for MVP:**
- Full bidirectional graph visualisation
- Full visual lineage graphs
- Multi-channel delivery
- Complex triggers (every initiative update, cross-entity simulations)
- Time-travel causal view
- Decision Graveyard auto-enrichment

## Dependencies
- Assumption Review & Evidence System — **complete**
- Strategic Evolution & Time-Travel (98% complete)
- Radar MVP Infrastructure & MCP (in progress)
- Strategic Actions entity — **complete** (for Phase 2.5 action linking)

## Key Risks

| Risk | Likelihood | Impact | Mitigation |
|------|-----------|--------|------------|
| Users ignore or distrust alerts | High | Critical | Start with max 1-2 high-signal alerts per week; make each undeniably useful |
| Causal chains are plausible but wrong | Medium | High | Human feedback loop on every alert; inline correction mechanism |
| Drift alerts feel low-urgency / ignorable | Medium | Medium | Only fire on high-impact assumptions with significant provenance decay |
| Drift detection flags everything (thin evidence base) | Medium | High | Gate drift triggers on Assumption Review completion; require minimum evidence threshold |
| Alert fatigue / noise | Medium | Medium | High-impact assumptions only; tunable thresholds |
| Over-reliance on AI recommendations | Low | High | All meaningful changes require explicit human confirmation |
| Chain snapshots grow large over time | Low | Low | Soft-delete superseded snapshots after 90 days; JSONB compression |

## Operating Rhythm (System Does the Work)

- **Daily:** Advisor surfaces only what actually needs attention. No forced review sessions.
- **Weekly:** A short Pulse summary of causal intelligence and drift status if anything meaningful happened. If nothing important occurred, the system stays quiet.
- **Goal:** Zero extra meetings for users who trust the system.

## Strategic Alignment

Directly supports:
- Strategic Intelligence (primary home)
- Strategic Evolution & Time-Travel
- Product Architecture — Strategic AI Infrastructure
- Category Leadership + Product-Market Fit
- Coach Network GTM + Advisory Firms as Customer Segment
- Funding & Growth (Seed Fundraise narrative)
- Strategic Actions initiative (causal chain snapshots enable action→chain linking)

## Book Connection

This initiative is the operational backbone of Chapter 6 (Strategic Intelligence) and Chapter 9 (From Periodic to Continuous Alignment). The silent drift detection specifically strengthens Chapter 4 (From Documents to Systems) — reinforcing the "workspace as state" and "consumption keeps it alive" concepts.
