---
id: a2a17a3a-240c-4179-86b5-292f12862472
type: decision
decisionType: type_1_irreversible
status: decided
decidedAt: 2026-01-30T12:52:38.611+00:00
lastUpdated: 2026-01-30T12:52:38.673902+00:00
---

# Role-Aware Strategic Intelligence as Core Architecture

## Description
Decide whether to build one unified system with role-aware interfaces (CEO gets Strategic Advisor, board gets Strategic Interface, managers get Strategic Coach, ICs get Strategic Guide) vs. separate products per persona. This is a fundamental architectural bet that affects product development, go-to-market, and positioning.

## Details
- **Type**: Type 1 (Irreversible)
- **Status**: decided
- **Authority**: Founder
- **Deadline**: No deadline
- **Decided At**: 2026-01-30T12:52:38.611+00:00

## Context
Current state (Jan 27, 2026): Strategic Advisor (founder mode) in daily use, validated through dogfooding. No other role interfaces built yet. Context Packaging Engine starting development with Feb 10 target.

GTM context: ScaleUp Company as first lighthouse customer (Phase 1 starts post-Feb 10). Sequoia pitch window April 2026. Customer meetings begin Feb 16.

The architectural question resolved: Build one unified system with role-aware modes vs. separate products per persona.

Original framing had 7 distinct interfaces (Advisor, Interface, Demo, Partner, Coach, Guide). Simplification analysis showed: 7 separate interfaces = divergence risk, more complexity, feels like different products. 1 interface with role modes = stays unified, less complexity, one product that adapts.

Implementation approach: System knows user role (founder, prospect, investor, manager, IC). Same underlying prompt architecture. Role context flag adapts: tone, access, agency, capture.

Phased rollout planned:
- Phase 1 (now): Founder mode ✓
- Phase 1b (Q1): Prospect mode for lighthouse demos
- Phase 2 (Q2): Investor/Board mode for Sequoia
- Phase 3 (Q3-Q4): Manager/IC modes if demand validated

Key assumptions being validated:
- A26: Organizations want strategy accessible beyond executives (75% confidence)
- A27: Role-aware modes increase adoption vs one-size-fits-all (70% confidence)
- A29: Prospects convert better with their own context (85% confidence)
- A31: One interface with modes is simpler than separate interfaces (90% confidence)

## Research
No research recorded

## Decision
Build one unified system with role-aware modes rather than separate products per persona. Single interface adapts based on user role through Context Packaging Engine. Role context flags control tone, access, agency, and insight capture. Phased rollout: Founder mode (now) → Prospect mode (Q1) → Investor mode (Q2) → Team modes (Q3-Q4, demand-dependent).

## Rationale
1. Complexity reduction: 7 separate interfaces = 7 prompt architectures, divergence risk, maintenance burden. 1 interface with role modes = unified system, single prompt with role context.

2. User experience: Prospect using "prospect mode" feels like they're using the real product, not a demo version. This supports "demo is the product" principle.

3. Moat creation: Operational lock-in across roles is stronger than single-user adoption. When founder uses Advisor, board uses Interface, managers use Coach — switching means changing how the company operates.

4. Defensibility: AI giants (Microsoft, Salesforce) will build one-size-fits-all. Role-aware architecture with different permissions, tones, and agencies is structurally different and hard to replicate.

5. Feedback loop multiplication: Different roles capture different signals — founder captures strategic decisions, managers capture execution friction, ICs capture ground-level reality, prospects capture buying signals. Whole org becomes sensing system.

6. Validation approach: Prove pattern with prospect mode first (ScaleUp demo), then extend. Don't build team modes until demand validated through lighthouse customers.

## Outcome
No outcome recorded yet
