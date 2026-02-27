---
id: 638c159e-e643-4b1e-8dec-d62428ba2108
type: initiative
status: in_progress
priority: high
strategy: Strategic Intelligence
completionPercentage: 0
lastUpdated: 2026-02-27T16:22:53.883+00:00
owner: af04d126-d28a-43a7-be8b-0c9451873f1b
---

# Strategic Alignment Suite

## Description
Productize the complete set of alignment tools as an integrated suite — four lenses on the same living strategy, powered by Stratafy's structured strategic context layer.

THE FOUR ALIGNMENT TOOLS:

1. Foundation Alignment (Vertical) — Strategies measured against mission, vision, values, beliefs, principles. Catches philosophical drift. STATUS: Live.

2. Strategic Coherence (Horizontal) — Portfolio-level check ensuring strategic bets aren't pulling in opposite directions. Catches internal conflict and resource tension. STATUS: Planned.

3. Radar Scanning (Outside-In) — Continuous external monitoring filtered through strategic context. Catches when assumptions break or opportunities emerge. STATUS: Live.

4. Public Presence Alignment (Inside-Out) — Evaluates external expression against strategic intent. Catches the gap between stated strategy and market-facing reality. STATUS: Proven with STIR (Feb 2026).

WHY COMPLETE: Vertical + Horizontal + Inbound + Outbound = every direction of misalignment covered. All four share the same engine — Stratafy's structured strategic context. No other tool offers this integrated.

MAPS TO FOUR-SCAN MODEL: Alignment Scan = Intent, Organigram Scan = Capacity (future), Radar Scan = Reality, Public Narrative Scan = Perception.

PITCH: "Stratafy doesn't just store strategy — it uses strategic context programmatically to evaluate whether your organization is aligned internally, coherent across strategies, oriented to reality, and perceived correctly. Continuously."

## Parent Strategy
[Strategic Intelligence](../strategy/functional/strategic-intelligence.md)

## Status & Progress
- **Status**: in progress
- **Priority**: high
- **Completion**: 0%

## Key Objectives
- [Internal Alignment Scan — demo-ready](../objectives/internal-alignment-scan-demo-ready.md)
- [Strategic Coherence Scan — demo-ready](../objectives/strategic-coherence-scan-demo-ready.md)
- [Radar Scan — demo-ready with Global Access example](../objectives/radar-scan-demo-ready-with-global-access-example.md)
- [Public Presence Alignment Scan — demo-ready](../objectives/public-presence-alignment-scan-demo-ready.md)
- [Cowork Plugin — workspace creation with Scaling Up artifacts](../objectives/cowork-plugin-workspace-creation-with-scaling-up-artifacts.md)

## Timeline
- **Start Date**: 2026-02-18
- **Target Date**: 2026-03-06

## Content
## Strategic Alignment Suite — Five Directional Lenses on Strategic Drift

The Strategic Alignment Suite is the complete system for detecting and correcting strategic drift. Five directional lenses, each catching a different class of misalignment, all operating on the same living strategy.

Methodology reference: Part 2 of 7 — Strategic Alignment (`/methodology/strategic-alignment`)

### The Five Lenses

| # | Lens | Direction | What It Checks | Initiative | Status |
|---|------|-----------|----------------|------------|--------|
| 1 | **Internal Alignment** | Vertical (Foundation ↔ Strategy) | Do strategies reflect mission, vision, values, beliefs, principles? | Alignment Scan MVP | MVP built |
| 2 | **Strategic Coherence** | Horizontal (Strategy ↔ Strategy) | Do strategies reinforce or contradict each other? | Strategic Coherence Scan | Draft |
| 3 | **Radar Scanning** | Inbound (External ↔ Strategy) | Is the world changing in ways that validate or invalidate strategy? | Radar MVP (separate project) | In Progress |
| 4 | **Public Presence** | Outbound (Strategy ↔ External Expression) | Does market-facing expression match strategic intent? | Public Narrative Alignment Scan | Draft |
| 5 | **Organizational** | Structural (Strategy ↔ People & Structure) | Right people, roles, capabilities, structure to execute? | Organigram-Strategy Alignment Scan | Draft |

### Architecture

All scan types (except Radar) share the same database tables:
- `strategy_reviews` — one row per scan, discriminated by `review_type`
- `review_perspectives` — findings per scan, discriminated by `perspective_type`
- `review_comments` — discussion threads on findings

Review type values: `alignment_scan`, `coherence_scan`, `presence_scan`, `org_scan`

### Synthesis Layer

The **Strategic Review Reports** project (STR-94 → STR-98) sits above all scan types as the synthesis layer — aggregating individual scans into consolidated executive reports with cross-cutting insights and actionable recommendations.

### Related Initiatives

- **Alignment Scan MVP** (Product-Market Fit) — Lens 1, foundation alignment. Built.
- **Strategic Coherence Scan** (Product Architecture) — Lens 2, strategy-vs-strategy. Next priority.
- **Radar MVP** (Strategic Intelligence) — Lens 3, external environment. Separate project.
- **Public Narrative Alignment Scan** (Product-Market Fit) — Lens 4, outbound expression. Draft.
- **Organigram-Strategy Alignment Scan** (Product Architecture) — Lens 5, organizational fit. Draft.

### Future Extensions

- `[FUTURE] Cultural & Values Coherence Sensing` — deeper layer of Lens 1
- `[FUTURE] Dependency & Sequencing Intelligence` — deeper layer of Lens 2
- `[FUTURE] Stakeholder Alignment Mapping` — deeper layer of Lens 5
