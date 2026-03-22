---
id: 7cf32226-ec43-4a7d-bd4f-06c8b0a9f4b3
type: strategy
status: active
strategyType: product
parent: 0a24cfc9-4e6d-48dc-9a0b-9f4f951a4222
---

# Strategic Delivery

## Description
How strategic intelligence reaches the right person, in the right way, on the right surface. Unifies four previously separate concerns: the role-aware persona model (who sees what), AI expert personas (CTO, CFO, CMO etc.), the conversational interaction layer (how intelligence is presented), and multi-platform surface adapters (Slack, Teams, Google Chat, web). One strategy for getting intelligence from the system to the human — whether that's a CEO morning briefing on WhatsApp, a CTO plugin in Claude, or a strategy summary card in Slack.

## Content
# Role-Aware Strategic Intelligence

## Strategic Intent

**Question answered**: How do we make strategy accessible to everyone in an organization, not just executives?

**Answer**: The same underlying strategic context adapts based on who you are and what you need. One strategy tree, many role-appropriate lenses.

**Time Horizon**: Q1-Q4 2026 (phased rollout)

**Strategic Theme**: One strategic system, many role-appropriate contexts. This strategy defines the intelligence layer — how context is scoped, tone adapts, access is governed, and signals are captured per role. The Stratafy Leadership Team strategy defines the delivery mechanism — Claude Cowork plugins that consume this context layer.

---

## Relationship to Stratafy Leadership Team

This strategy and the Stratafy Leadership Team are two sides of the same coin:

| This Strategy (Role-Aware Intelligence) | Leadership Team Strategy |
|----------------------------------------|--------------------------|
| Defines the context layer | Defines the delivery mechanism |
| What each role sees, how it speaks, what it captures | The actual plugins people install and interact with |
| Role-scoping architecture | Named executive personas (CFO, COO, CMO) |
| Access levels, tone, agency, capture rules | Commands, skills, authority boundaries, pricing |

Without role-aware context, the Leadership Team plugins are just different prompt wrappers. With it, they're genuinely scoped executives that share one strategy tree but see it through their role's lens.

**Every Leadership Team plugin depends on this context layer to function properly.**

---

## Origin

This strategy emerged from a roleplay exercise simulating an investor update call. The exercise revealed that the "Strategic Advisor" concept is one instance of a broader pattern: role-aware interfaces to the same underlying strategic system.

The insight: **The system should understand your role and interact with you accordingly.**

## The Core Architecture

```
┌─────────────────────────────────────────────────────┐
│           STRATAFY STRATEGIC SYSTEM                 │
│  Foundation │ Strategies │ Insights │ Feedback Loop │
└─────────────────────────────────────────────────────┘
                         │
              ┌─────────────────────┐
              │  Role-Aware Context │
              │       Layer         │
              └─────────────────────┘
                         │
         ┌───────┬───────┼───────┬───────┐
         ▼       ▼       ▼       ▼       ▼
      Finance  Team    COO     CMO    CEO-mode
      Director Partner (planned)(planned)(planned)
      Plugin   Plugin
         │       │       │       │       │
         ▼       ▼       ▼       ▼       ▼
       CFO     Coach/  Ops    Marketing Strategic
       Context Manager Context Context  Advisor
              Context                   Context
```

One system. One strategy tree. Role-aware context layer. Multiple plugin delivery points.

## What Adapts By Role Context

| Dimension | How It Adapts |
|-----------|---------------|
| **Access** | What strategies, insights, and data are visible to this role |
| **Tone** | Founder: challenging. Team member: coaching. Board: concise |
| **Agency** | Founder: full edit. Manager: team-scoped edit. IC: read + capture |
| **Capture** | Founder insights → strategy. Manager observations → execution friction. IC feedback → ground-level reality |
| **Guidance** | Founder: minimal. Manager: translates strategy to team context. IC: connects work to meaning |

## Context Enforcement: The Depth/Access Model

The context layer is enforced through a structured system that controls two dimensions per entity per role:

**Depth** (what you see): Full → Executive → Brief → Reference → Excluded. Each level returns progressively less content, from complete strategy documents down to just a name and status. This also manages AI token budgets — a Finance Director gets full financial strategy content but only a brief summary of marketing strategies.

**Access** (what you can do): Write → Suggest → Read → None. "Suggest" is the key innovation — roles with suggest-level access can propose changes that route to an approval queue, enabling cross-executive collaboration without breaking authority boundaries. A Finance Director can propose budget changes on an initiative; the COO approves.

This layers on top of existing RBAC permissions as a soft intelligence boundary. Permissions handle security (can/can't); context profiles handle relevance (what depth, what scope). Context profiles can only reduce what permissions allow, never escalate.

> The full technical specification including data model, MCP integration, UI surfaces, and default profiles per executive role is preserved in the "Role Context System — Technical Specification" document.

## Role Context Mapping to Leadership Team Plugins

| Role Context | Leadership Team Plugin | Status |
|-------------|----------------------|--------|
| Founder/CEO strategic context | Stratafy Coach (stratafy-cowork v1.3.0) | Live |
| CFO/financial context | Stratafy Finance Director (stratafy-finance v0.3.0) | Live |
| Team member/manager context | Stratafy Team Partner (stratafy-team v0.1.0) | Beta |
| Operations/initiative context | Stratafy COO (planned) | Q2 2026 |
| Marketing/positioning context | Stratafy CMO (planned) | Q2 2026 |
| Strategic oversight context | Stratafy CEO-mode (planned) | Q3 2026 |
| People/culture context | Stratafy CHRO (planned — potential We Are 52 co-build) | Q3 2026 |

## Phased Context Rollout

### Phase 1: Now — Foundation Contexts
- **Founder context** — Full Strategic Advisor, in daily use ✅
- **CFO context** — Financial intelligence scoped to strategy-spend alignment ✅
- **Team member context** — Role-adaptive execution partner, beta ✅

### Phase 2: Q2 2026 — Operational Contexts
- **Operations context** — Initiative tracking, OKR management, bottleneck detection
- **Marketing context** — Content alignment, positioning governance, channel performance
- **Prospect context** — Educational tone, explains concepts, surfaces value. Demo-as-product.
- **Investor/Board context** — Transparent status, governance focus, Sequoia updates

### Phase 3: Q3-Q4 2026 — Expanded Contexts (Validated by Channel Exploration)
- **Manager/Coach context** — Translates strategy to team. Explains "why." Coaches through questions.
- **IC/Guide context** — Connects individual work to meaning. Answers "how does my work connect?"
- **People/culture context** — People strategy, org health, talent planning (CHRO plugin)

**GTM dependency note**: The advisory firm and coach network GTM channels are currently in exploration mode. When those channels graduate to committed execution (see GTM Channels graduation criteria), they will require Manager/Coach and IC contexts to be production-ready so coaches can deploy Leadership Teams to their clients' organizations. Channel exploration signals should inform the design of these contexts — every conversation with a coach or advisory firm is a data point about what team contexts need to do.

## The Prospect Context: Demo as Product

### The Insight

The best demo isn't a pitch — it's the product with more guidance. When a prospect uses Stratafy:

1. **Same interface** — They're using the real product
2. **Educational tone** — System explains concepts as it uses them
3. **Their data** — Pre-populated workspace with their context
4. **Value surfaces naturally** — Alignment gaps on THEIR strategy

### Demo Prep (Lighthouse Only)

For 2-3 lighthouse customers, invest 2-3 hours each:

| Element | Source | Purpose |
|---------|--------|---------|
| Mission/Vision | Website, pitch deck | Shows we did homework |
| Values | Culture page, inferred | Starting point |
| 2-3 Strategies | Public info, discovery call | Real context to analyze |

**This is not scalable and doesn't need to be.** Once ScaleUp Company succeeds, subsequent customers require less convincing. Templates and patterns emerge. The motion gets lighter.

### Buying Signals to Capture

Prospect context captures (as insights):
- Pain indicators ("Can it catch when teams go off-strategy?")
- Reactions to gaps ("That's exactly our problem")
- Feature requests ("Can it also do X?")
- Objections ("How is this different from OKRs?")
- Stakeholder mentions ("I'd need to show our VP Eng")

These inform sales AND product.

## Why This Matters

### 1. Strategy Becomes Accessible
Most employees never see strategy beyond an all-hands deck. Role contexts make strategic context queryable for everyone.

### 2. Feedback Loop Multiplies
Different roles capture different signals:
- Founder: strategic decisions
- Manager: execution friction
- IC: ground-level reality
- Prospect: buying signals, pain points

The organization becomes a sensing system.

### 3. Operational Lock-In
Once founder uses the Coach daily, the CFO monitors financial alignment, the COO tracks initiatives, and managers use the Team Partner — switching means changing how the company operates. That's the moat.

### 4. Defensible Against AI Giants
Microsoft/Salesforce will build one-size-fits-all. Role-aware contexts with different permissions, tones, and agencies is architecturally different. Hard to replicate because the context layer requires deep strategic architecture, not just prompt engineering.

## ScaleUp Company: The Validation Partner

ScaleUp Company is not just a customer. They're the validation partner for this entire strategy.

**If ScaleUp Company converts and succeeds:**
- Case study for sales
- Reference for subsequent prospects
- Proof that demo-as-product works
- First organization to test team role contexts
- Sequoia pitch has teeth

**Over-invest in their success. Their win is Stratafy's win.**

## Success Criteria

### Phase 1 (Foundation Contexts)
- [x] Founder context in daily use
- [x] CFO context shipped (stratafy-finance v0.3.0)
- [ ] Team member context validated with beta users

### Phase 2 (Operational Contexts)
- [ ] Operations context built (COO plugin)
- [ ] Marketing context built (CMO plugin)
- [ ] Prospect context tested in lighthouse demos
- [ ] Investor context used for Sequoia updates

### Phase 3 (Expanded Contexts)
- [ ] Manager/Coach context tested with real managers (ScaleUp Company)
- [ ] IC context tested with real ICs
- [ ] GTM channel exploration signals incorporated into context design
- [ ] Adoption rate measured: Leadership Team vs founder-only

## Strategic Constraints

- Every role context MUST share the same strategy tree — no siloed intelligence
- Context scoping MUST be explicit — what you see, what you can do, what gets captured
- We do NOT build expanded role contexts before demand is validated through channel exploration
- We do NOT compromise authenticity for role-appropriateness (no spin layer)
- Context design MUST be informed by real conversations with coaches, advisory firms, and team members

## Key Assumptions

| ID | Assumption | Confidence | Validation |
|----|------------|------------|------------|
| A26 | Organizations want strategy accessible beyond executives | 75% | ScaleUp Company feedback on team contexts |
| A27 | Role-aware contexts increase adoption vs one-size-fits-all | 70% | Usage comparison post-Phase 3 |
| A29 | Prospects convert better when demo uses their context | 85% | First 3 lighthouse demos |
| A31 | One system with role contexts is simpler than separate products | 90% | Implementation effort |

## Relationship to Other Strategies

- **Parent**: Product Architecture — core architectural pattern
- **Sibling/delivery**: Stratafy Leadership Team — plugins that consume this context layer
- **Supports**: Product-Market Fit — expands value beyond founder
- **Supports**: Category Creation — "strategic intelligence for everyone"
- **Enables**: Funding & Growth — investor context for Sequoia
- **Enables**: GTM Channels — team contexts unblock coach and advisory channel execution
- **Informed by**: GTM channel exploration — every channel conversation is a data point for context design

## Key Initiatives
- [Multi-Channel Messaging — Google Chat, Telegram & WhatsApp Bots](../initiatives/multi-channel-messaging-google-chat-telegram-whatsapp-bots.md)
- [Stratafy Experts — Roster, Linking & Context Packaging](../initiatives/stratafy-experts-roster-linking-context-packaging.md)
- [Context Intelligence v2 — Query-Intent Routing & Adaptive Compression](../initiatives/context-intelligence-v2-query-intent-routing-adaptive-compression.md)
- [Stratafy Leadership Team — Cowork Plugins](../initiatives/stratafy-leadership-team-cowork-plugins.md)
- [AI-Powered Strategy Contribution & Approval Engine](../initiatives/ai-powered-strategy-contribution-approval-engine.md)
- [External Context Packaging](../initiatives/external-context-packaging.md)
- [[FUTURE] Stakeholder Alignment Mapping](../initiatives/future-stakeholder-alignment-mapping.md)
- [Agent Registry & API Key Platform](../initiatives/agent-registry-api-key-platform.md)

## Alignment Score
Not calculated

## Time Horizon
medium_term
