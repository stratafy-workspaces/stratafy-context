---
id: 80c96153-f401-4a2c-ad70-b7e5f4afdeda
type: insight
source: architecture_review
category: strategic
impactLevel: high
confidenceLevel: likely
status: pending
actionable: true
---

# Architecture is converging toward multi-tenant advisory infrastructure — workspace hierarchy is the unlock

## Summary
Five features built independently across 8 weeks form a coherent multi-tenant advisory system: user-scoped cross-workspace API keys, expert roster, guardian plugin, partner plugin layer (We Are 52), and the planned workspace hierarchy. The permission model needs "advisor sees strategy but not finance" granularity to unlock the advisory firm distribution channel.

## Description
## Maps To
- **Partner Plugin Ecosystem** strategy (direct enabler)
- **Core Product Capabilities** → Workspace Hierarchy initiative (start date April 2026)
- **Strategic Delivery** → Stratafy Experts initiative
- **Advisory Firms as Customer Segment** strategy
- **Fractional Executive & CSIO Channel** strategy

## Convergence Evidence
1. **User-scoped API keys** (Week 3) — cross-workspace access enabled
2. **Expert roster** (Week 8) — AI executives with strategy assignment
3. **Guardian plugin** (Week 7) — governance-focused plugin
4. **Partner plugin layer** (Week 7) — We Are 52 prototype
5. **Workspace Hierarchy** (planned April) — parent/child for portfolio insights

## Recommendation
When building Workspace Hierarchy, design the permission model with advisor-scoped access from the start — retrofitting is costly. Also plan for: advisor dashboards spanning workspaces, workspace templates, portfolio-level health score aggregation.

## Strategic Implication
If this model works, one advisory firm onboarding brings 10-50 client workspaces. The partner plugin ecosystem and guardian plugin are the tools, workspace hierarchy is the structure, cross-workspace API keys are the plumbing. It's already half-built.

## Classification
- **Source**: architecture review
- **Category**: strategic
- **Impact**: high
- **Confidence**: likely
- **Status**: pending
- **Actionable**: Yes
- **Tags**: multi-tenant, advisory-model, workspace-hierarchy, partner-ecosystem, permissions


