---
id: b5dfbe73-d493-43df-8dc9-a828facc23fb
type: strategy
status: active
strategyType: functional
parent: e5d9c6eb-d34b-4af5-a6e0-541d4beb6df2
lastUpdated: 2026-01-29T17:36:38.183+00:00
owner: af04d126-d28a-43a7-be8b-0c9451873f1b
---

# Sequoia Engagement

## Description
Convert Sequoia pitch into a product experience. Build demo workspaces (Sequoia + portfolio companies), craft Strategic Advisor prompt, and deliver a demo where Roelof experiences Stratafy as an investor evaluating companies — selling both Sequoia-level portfolio visibility and per-company strategic infrastructure.

## Content
# Sequoia Engagement Strategy

## Strategic Intent

**Question answered**: How do we convert the Sequoia pitch into a product experience that sells itself?

**Time Horizon**: Feb - April 2026

**Strategic Theme**: Don't pitch Stratafy — let Roelof experience it. Build demo workspaces where he sees his own portfolio through Stratafy's lens, connect him to a Strategic Advisor that reasons against real strategic context, and make the value undeniable.

## ⚠️ Demo Quality = Outcome

**Demo quality determines fundraising outcome. Invest disproportionate time.**

For experiential products, the demo IS the pitch. A slide deck cannot convey what Stratafy does. The only way to understand it is to feel it.

| Principle | Implication |
|-----------|-------------|
| Practice 10x minimum | Every edge case covered |
| Make it personal | Roelof's portfolio, not generic examples |
| Have backups | Screenshots, recordings, Plan B |
| Never wing it | Rehearsed transitions, scripted fallbacks |

The Sequoia meeting is the most leveraged 30 minutes of the next 90 days. Treat it that way.

## The Double Sale

This pitch must sell Stratafy twice:

| Audience | Their Question | Our Answer |
|----------|---------------|------------|
| **Roelof as VC** | "Why should Sequoia invest in this?" | "You could see strategic alignment across your entire portfolio" |
| **Roelof as board member** | "How does this help companies I advise?" | "Every board meeting becomes queryable, not just slides" |
| **Portfolio company CEO** | "Why should we use this?" | "Single source of truth for humans and AI" |
| **Sequoia as firm** | "Is this a category?" | "Every company will need this. First mover advantage is now." |

## The Demo Narrative

### Setup (1 min)
- Roelof connects Claude to Stratafy MCP (or screenshare)
- Brief context: "Let me show you what strategic infrastructure looks like"

### Act 1: Portfolio View (2 min)
> "Imagine you could ask: 'Which of my portfolio companies has the highest strategic drift risk right now?'"

- Show Sequoia workspace with 3-4 portfolio companies
- Each has foundation + strategies + alignment scores
- Surface which ones need attention
- **Sells**: Portfolio-level visibility Sequoia doesn't have today

### Act 2: Dive Into One Company (3 min)
> "Let's look at [Company X]. Their stated strategy is enterprise growth. But look — their initiatives are all SMB-focused. The AI caught this."

- Show company's Foundation (mission, values)
- Show Strategy layer with initiatives
- Run Alignment Scan, show the contradiction
- Show specific recommendations
- **Sells**: Per-company strategic coherence

### Act 3: Strategic Advisor (3 min)
> "Now ask Claude anything about this company's strategy."

- Roelof asks: "Should they pursue this acquisition?" or "What's the biggest risk to their Q3 goals?"
- Claude responds grounded in foundation, strategies, alignment data
- Not generic advice — specific to their context
- **Sells**: AI that reasons against strategic intent

### Act 4: The Close (2 min)
> "This is what Stratafy does. Every company you invest in could have this. You could have this across all of them. We're raising to make this the standard infrastructure for strategy execution."

- Brief pitch: market size, timing, team, ask
- But the product already made the case

## Product Requirements

### Must Have (by April)

| Capability | Status | Owner | Deadline |
|------------|--------|-------|----------|
| Alignment Scan working reliably | 🔨 In Progress | Leonard | Feb 10 |
| Strategic Advisor system prompt | 🔴 Not Started | Leonard | March 15 |
| Demo workspaces populated | 🔴 Not Started | Leonard | March 31 |
| MCP auth for external user (or screenshare fallback) | ❓ Check | Leonard | March 15 |
| Smooth demo flow (no crashes, fast) | — | Leonard | April 1 |

### Nice to Have

| Capability | Value | Complexity |
|------------|-------|------------|
| Workspace hierarchy (Sequoia → Portfolio) | Visual parent-child | Medium |
| Portfolio-level alignment dashboard | "Which companies are drifting?" | High |
| Roelof can connect his own Claude | Maximum impact | Medium |

### Won't Have (for this demo)

- Full portfolio of 50+ companies
- Real Sequoia data (use public + hypothetical)
- Enterprise features (SSO, audit logs)

## Demo Preparation Checklist

**2 weeks before:**
- [ ] All workspaces populated and reviewed
- [ ] Demo script finalized
- [ ] Alignment Scan running reliably
- [ ] Strategic Advisor prompt tested

**1 week before:**
- [ ] Full run-through recorded
- [ ] Backup screenshots captured
- [ ] Edge cases identified and scripted
- [ ] 1-pager sent to Pieter for forwarding

**Day before:**
- [ ] Fresh test of entire flow
- [ ] Backup laptop ready
- [ ] Mobile hotspot charged
- [ ] Calendar blocked for 2 hours before

**Day of:**
- [ ] 30-min warmup rehearsal
- [ ] Close unnecessary apps
- [ ] Water, notes ready
- [ ] Deep breath

## Content Requirements

### Workspaces to Build

| Workspace | Purpose | Data Source |
|-----------|---------|-------------|
| **Sequoia Capital** | Show VC use case | Public info + hypothetical |
| **Portfolio Company 1** (MongoDB) | Roelof board seat, data available | Public filings, investor materials |
| **Portfolio Company 2** (Block/Square) | Roelof board seat, complex strategy | Public filings, investor materials |
| **Portfolio Company 3** (Hypothetical/Anonymized) | Show misalignment scenario | Constructed to show value |
| **Stratafy** | ✅ Already built | Your own dogfood |

### Sequoia Workspace Content

**Mission** (hypothetical, based on public positioning):
> "Help the daring build legendary companies"

**Vision**:
> "Identify and partner with exceptional founders at every stage, from seed to growth, building category-defining companies"

**Values** (inferred from their actions/content):
- Founder-first over Deal-first
- Long-term partnership over Transactional capital
- Concentrated bets over Diversification
- Hands-on support over Passive investment

**Strategies**:
- Early-stage sourcing (scouts, network)
- Growth investing
- Portfolio support (talent, ops, go-to-market)
- Sector focus (AI, fintech, healthcare, etc.)

### Portfolio Company Workspace Content

For each company (MongoDB, Block):
1. Research public mission/vision statements
2. Extract values from culture pages, earnings calls
3. Map strategies from investor presentations
4. Create plausible initiatives from public announcements
5. Run alignment scan to find interesting tensions

**Goal**: Find a real (or realistic) misalignment to surface in demo. "Their stated value is X, but their strategy does Y."

## Strategic Advisor Prompt

This is the system prompt that makes Claude reason against the workspace.

### Prompt Structure

```
You are a Strategic Advisor with deep knowledge of {company_name}'s strategy.

## Your Knowledge Base

You have access to this organization's complete strategic context via MCP:

### Foundation (Who They Are)
- Mission: {loaded from workspace}
- Vision: {loaded from workspace}
- Values: {loaded from workspace}
- Beliefs: {loaded from workspace}
- Principles: {loaded from workspace}

### Strategy (Where They're Going)
- Corporate strategies: {loaded}
- Functional strategies: {loaded}
- Initiatives: {loaded}
- Alignment scores: {loaded}

### Recent Analysis
- Latest alignment scan results: {loaded}
- Key misalignments flagged: {loaded}
- Recommendations pending: {loaded}

## Your Role

You are advising {user_role} on strategic questions.

When answering:
1. Ground every response in the actual foundation and strategy data
2. Reference specific values, beliefs, or principles when relevant
3. Flag when a question touches on a known misalignment
4. Be direct about strategic risks or contradictions
5. Recommend actions that strengthen alignment

When you don't have enough context:
- Say so clearly
- Suggest what additional strategic clarity would help
- Offer to run an alignment scan if relevant

## Your Tone

- Confident but not arrogant
- Grounded in data, not generic advice
- Willing to challenge assumptions
- Focused on strategic coherence

## What You Don't Do

- Make up information not in the workspace
- Give generic business advice unconnected to this company's strategy
- Ignore misalignments to be polite
- Pretend certainty when data is incomplete
```

### Per-Audience Variants

| User Role | Prompt Adjustment |
|-----------|-------------------|
| **Investor (Roelof)** | Focus on risk, execution confidence, strategic clarity |
| **CEO** | Focus on alignment, team execution, prioritization |
| **Board member** | Focus on oversight, drift detection, accountability |

## Relationship Strategy

### The Pieter Path

```
Current State → Warm intro request → Pieter agrees → Intro to Roelof → Demo meeting
```

| Step | Action | Timing |
|------|--------|--------|
| 1. Prep | Build demo, refine pitch | Feb-March |
| 2. Request | Ask Pieter for intro | Late March |
| 3. Context | Give Pieter the 2-min version to share | With request |
| 4. Intro | Pieter makes connection | April |
| 5. Demo | 30-min meeting with Roelof | April-May |

### What Pieter Needs to Say

> "Leonard is building strategic infrastructure for the AI era. He's got something I think you should see. It's relevant to how you think about portfolio company execution."

Short, credible, specific.

### Pre-Meeting Warmup

Before the demo meeting:
- Roelof receives a 1-pager (problem, solution, why now)
- Link to Stratafy blog articles (credibility)
- Optional: "I built a workspace for [Company] you're on the board of. Want to see it?"

## Success Criteria

| Criteria | Target |
|----------|--------|
| Demo runs without technical issues | 100% |
| Roelof asks follow-up questions | 3+ |
| Roelof says "this is interesting" or equivalent | Yes |
| Meeting leads to second conversation | Yes |
| Term sheet conversation within 60 days | Stretch |

## Risks & Mitigations

| Risk | Likelihood | Mitigation |
|------|------------|------------|
| Pieter doesn't make intro | Low (relationship is strong) | Backup paths: a16z, Greylock, SA investors |
| Demo fails technically | Medium | Practice 10x, have backup screenshots |
| Roelof doesn't see the vision | Medium | Tailor to his portfolio, make it personal |
| Product not ready in time | Medium | Cut scope, prioritize demo flow over features |
| Misalignment examples feel contrived | Medium | Use real public data, don't over-construct |

## Timeline

| Date | Milestone |
|------|-----------|
| Feb 10 | Alignment Scan MVP complete |
| Feb 15 | Strategic Advisor prompt v1 drafted |
| Feb 28 | Sequoia workspace populated |
| March 15 | Portfolio company workspaces populated |
| March 15 | Demo flow rehearsed, MCP access tested |
| March 31 | Demo ready for external use |
| Late March | Request intro from Pieter |
| April | Demo meeting with Roelof |

## Key Assumptions

| ID | Assumption | Confidence | Validation |
|----|------------|------------|------------|
| A16 | Product demo is more compelling than slide deck | 80% | Industry norm for dev tools |
| A17 | Roelof will engage if demo is relevant to his portfolio | 70% | His reputation for hands-on |
| A18 | Public company data is sufficient for realistic demo | 75% | Research quality |
| A6 | Pieter will make Sequoia introduction | 70% | Relationship strength |

## Strategic Constraints

What this strategy constrains:

- We do NOT pitch without a working demo
- We do NOT use fake data that could embarrass us
- We do NOT over-promise features not yet built
- We do NOT let demo prep delay product development (parallel tracks)
- We do NOT approach Roelof cold — only through Pieter
- **We do NOT wing the demo — practice 10x minimum**

## Next Actions

| Action | Owner | Deadline |
|--------|-------|----------|
| Complete Alignment Scan MVP | Leonard | Feb 10 |
| Draft Strategic Advisor prompt v1 | Leonard | Feb 15 |
| Research MongoDB strategic context | Leonard | Feb 20 |
| Research Block/Square strategic context | Leonard | Feb 25 |
| Build Sequoia workspace | Leonard | Feb 28 |
| Build portfolio company workspaces | Leonard | March 15 |
| Test full demo flow end-to-end | Leonard | March 20 |
| Rehearse demo 10x | Leonard | March 25 |
| Prepare 1-pager for Pieter | Leonard | March 25 |
| Request intro from Pieter | Leonard | Late March |
| Demo meeting with Roelof | Leonard | April |

## Key Initiatives
No initiatives defined

## Alignment Score
Not calculated

## Time Horizon
short_term
