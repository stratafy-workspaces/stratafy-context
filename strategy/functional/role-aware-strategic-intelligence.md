---
id: 7cf32226-ec43-4a7d-bd4f-06c8b0a9f4b3
type: strategy
status: active
strategyType: functional
parent: 0a24cfc9-4e6d-48dc-9a0b-9f4f951a4222
lastUpdated: 2026-01-30T14:03:04.321+00:00
owner: af04d126-d28a-43a7-be8b-0c9451873f1b
---

# Role-Aware Strategic Intelligence

## Description
One strategic system, many role-appropriate interfaces. The same underlying context (foundation, strategies, insights, feedback loop) adapts based on who you are — CEO gets Strategic Advisor, board gets Strategic Interface, managers get Strategic Coach, ICs get Strategic Guide. This is not a feature; it's a foundational architecture that makes strategy accessible at every level and multiplies the feedback loop across the entire organization.

## Content
# Role-Aware Strategic Intelligence

## Strategic Intent

**Question answered**: How do we make strategy accessible to everyone in an organization, not just executives?

**Time Horizon**: Q1-Q4 2026 (phased rollout)

**Strategic Theme**: One strategic system, many role-appropriate interfaces. The same underlying context adapts based on who you are and what you need.

## Origin

This strategy emerged from a roleplay exercise simulating an investor update call. The exercise revealed that the "Strategic Advisor" concept is one instance of a broader pattern: role-aware interfaces to the same underlying strategic system.

The insight: **The system should understand your role and interact with you accordingly.**

## Implementation Simplification (Jan 27, 2026)

**Don't build 7 separate interfaces. Build one interface with role-aware modes.**

The original framing described 7 distinct interfaces (Advisor, Interface, Demo, Partner, Coach, Guide). The simplified implementation:

| Original Framing | Simplified Implementation |
|------------------|---------------------------|
| 7 separate interfaces | 1 interface with role modes |
| 7 prompt architectures | 1 prompt with role context |
| Divergence risk over time | Stays unified |
| More complexity to build/maintain | Less complexity |
| Feels like different products | Feels like one product that adapts |

**How it works:**
- System knows user's role (founder, prospect, investor, manager, IC)
- Same underlying prompt architecture
- Role context flag adapts: tone, access, agency, capture
- Prospect feels like they're using the real product, not a demo version

**This is the "one system, many interfaces" principle applied to implementation**, not just architecture.

## The Core Architecture

```
┌─────────────────────────────────────────────────────┐
│           STRATAFY STRATEGIC SYSTEM                 │
│  Foundation │ Strategies │ Insights │ Feedback Loop │
└─────────────────────────────────────────────────────┘
                         │
                         ▼
              ┌─────────────────────┐
              │  Strategic Advisor  │
              │   (One Interface)   │
              └─────────────────────┘
                         │
         ┌───────┬───────┼───────┬───────┐
         ▼       ▼       ▼       ▼       ▼
      Founder  Prospect Investor Manager  IC
       Mode     Mode     Mode    Mode   Mode
```

One system. One interface. Multiple modes. Each adapted to role, access level, and purpose.

## Role-Mode Mapping

| Role | Mode | Primary Purpose | Tone Adaptation |
|------|------|-----------------|-----------------|
| **Founder/CEO** | Default | Think, decide, shape strategy | Challenging, direct, full context |
| **Prospect** | Demo | Experience Stratafy value | Educational, explains concepts, shows value |
| **Investor/Board** | Interface | Monitor, govern, advise | Transparent, concise, status-focused |
| **Manager** | Coach | Translate strategy to team | Explains "why," develops thinking |
| **IC** | Guide | Execute within context | Answers "how does my work connect?" |

## What Adapts By Role Mode

| Dimension | How It Adapts |
|-----------|---------------|
| **Access** | What strategies and insights are visible |
| **Tone** | Founder: challenging. Prospect: educational. Board: concise |
| **Agency** | Founder: full edit. Prospect: explore. Board: read + capture |
| **Capture** | Founder insights → strategy. Prospect questions → buying signals |
| **Guidance** | Founder: minimal. Prospect: explains as it goes. IC: connects to meaning |

## Phased Rollout (Simplified)

### Phase 1: Now
- **Founder mode** — Full Strategic Advisor, in daily use ✅

### Phase 1b: Q1 2026 (Next Priority)  
- **Prospect mode** — Same interface, educational tone, explains concepts
- High-touch prep for 2-3 lighthouse customers only
- Not a scalable sales motion — do things that don't scale

### Phase 2: Q2 2026 (Post-Funding)
- **Investor/Board mode** — Transparent status, governance focus
- First external stakeholder interface
- Sequoia using this for updates

### Phase 3: Q3-Q4 2026 (With Lighthouse Validation)
- **Manager mode** — Translates strategy to team context
- **IC mode** — Connects individual work to meaning
- Requires lighthouse customer testing (ScaleUp Company)
- Only build if demand validated

## The Prospect Mode: Demo as Product

### The Insight

The best demo isn't a pitch — it's the product with more guidance. When a prospect uses Stratafy:

1. **Same interface** — They're using the real product
2. **Educational tone** — System explains concepts as it uses them
3. **Their data** — Pre-populated workspace with their context
4. **Value surfaces naturally** — Alignment gaps on THEIR strategy

### Why This Works

| Separate Demo Product | Prospect Mode |
|-----------------------|---------------|
| Feels like a sales tool | Feels like the real product |
| "Let me show you our demo" | "Let me show you YOUR strategy" |
| Value promised | Value proven |
| Objection: "Will it work for us?" | They've already seen it work |

### Demo Prep (Lighthouse Only)

For 2-3 lighthouse customers, invest 2-3 hours each:

| Element | Source | Purpose |
|---------|--------|---------|
| Mission/Vision | Website, pitch deck | Shows we did homework |
| Values | Culture page, inferred | Starting point |
| 2-3 Strategies | Public info, discovery call | Real context to analyze |

**This is not scalable and doesn't need to be.** Once ScaleUp Company succeeds, subsequent customers require less convincing. Templates and patterns emerge. The motion gets lighter.

### Buying Signals to Capture

Prospect mode captures (as insights):
- Pain indicators ("Can it catch when teams go off-strategy?")
- Reactions to gaps ("That's exactly our problem")
- Feature requests ("Can it also do X?")
- Objections ("How is this different from OKRs?")
- Stakeholder mentions ("I'd need to show our VP Eng")

These inform sales AND product.

## Why This Matters

### 1. Strategy Becomes Accessible
Most employees never see strategy beyond an all-hands deck. Role modes make strategic context queryable for everyone.

### 2. Feedback Loop Multiplies
Different roles capture different signals:
- Founder: strategic decisions
- Manager: execution friction  
- IC: ground-level reality
- Prospect: buying signals, pain points

The organization becomes a sensing system.

### 3. Operational Lock-In
Once founder uses Advisor daily, board uses Interface mode, managers use Coach mode — switching means changing how the company operates. That's the moat.

### 4. Defensible Against AI Giants
Microsoft/Salesforce will build one-size-fits-all. Role-aware modes with different permissions, tones, and agencies is architecturally different. Hard to replicate.

## ScaleUp Company: The Validation Partner

ScaleUp Company is not just a customer. They're the validation partner for this entire strategy.

**If ScaleUp Company converts and succeeds:**
- Case study for sales
- Reference for subsequent prospects
- Proof that demo-as-product works
- Customer to test manager/IC modes
- Sequoia pitch has teeth

**Over-invest in their success. Their win is Stratafy's win.**

## Success Criteria

### Phase 1b (Prospect Mode)
- [ ] Prospect mode prompt built
- [ ] First lighthouse demo uses prospect mode
- [ ] Conversion tracked vs. baseline

### Phase 2 (Investor Mode)
- [ ] Investor mode prompt built
- [ ] Sequoia receiving updates via Interface
- [ ] Board governance patterns captured

### Phase 3 (Team Modes)
- [ ] ScaleUp Company requests team access
- [ ] Manager mode tested with real managers
- [ ] IC mode tested with real ICs
- [ ] Adoption rate measured vs. founder-only

## Strategic Constraints

- We do NOT build separate interfaces — one interface, multiple modes
- We do NOT over-invest in demo prep — lighthouse only, then templates
- We do NOT build team modes before demand validated
- We do NOT compromise authenticity for role-appropriateness (no spin layer)
- We do NOT let mode complexity slow down core product shipping

## Key Assumptions

| ID | Assumption | Confidence | Validation |
|----|------------|------------|------------|
| A26 | Organizations want strategy accessible beyond executives | 75% | ScaleUp Company feedback on team modes |
| A27 | Role-aware modes increase adoption vs one-size-fits-all | 70% | Usage comparison post-Phase 3 |
| A29 | Prospects convert better when demo uses their context | 85% | First 3 lighthouse demos |
| A31 | One interface with modes is simpler than separate interfaces | 90% | Implementation effort |

## Next Actions

| Action | Deadline | Notes |
|--------|----------|-------|
| Build prospect mode prompt | Feb 2026 | Add role context to existing Advisor prompt |
| Test with next prospect | Next demo | ScaleUp Company or next lighthouse |
| Build investor mode prompt | Post-funding | For Sequoia updates |
| Test team mode interest | Q2 2026 | Ask ScaleUp Company explicitly |

## Relationship to Other Strategies

- **Parent**: Product Architecture — core architectural pattern
- **Supports**: Product-Market Fit — expands value beyond founder
- **Supports**: Category Creation — "strategic intelligence for everyone"
- **Enables**: Funding & Growth — investor mode for Sequoia
- **Enables**: Sales — prospect mode makes demo = product

## Key Initiatives
- [Context Packaging Engine](../initiatives/context-packaging-engine.md)
- [Agent Registry & Context Packaging](../initiatives/agent-registry-context-packaging.md)
- [[FUTURE] Stakeholder Alignment Mapping](../initiatives/future-stakeholder-alignment-mapping.md)

## Alignment Score
Not calculated

## Time Horizon
medium_term
