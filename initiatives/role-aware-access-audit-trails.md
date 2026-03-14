---
id: 221976c1-b341-4fff-9342-9a48fe75312a
type: initiative
status: active
priority: medium
strategy: Strategic AI Infrastructure
completionPercentage: 0
---

# Role-Aware Access & Audit Trails

## Description
Build role-aware strategic views and decision audit trails. Role views: board member sees full strategy tree at summary level with health scores; product manager sees their initiative context with relevant objectives and risks; investor sees pitch view with key metrics and traction. Audit trails: who made which decisions, based on what intelligence, when. Creates institutional memory and meets enterprise compliance requirements. Prerequisite for SOC2/GDPR certification and enterprise pricing tier ($5K+/mo). Extends existing Supabase Auth and workspace-level access with strategy-aware granularity.

## Parent Strategy
[Strategic AI Infrastructure](../strategy/product/strategic-ai-infrastructure.md)

## Status & Progress
- **Status**: active
- **Priority**: medium
- **Completion**: 0%

## Key Objectives
- [Complete decision audit trail including AI interaction governance](../objectives/complete-decision-audit-trail-including-ai-interaction-governance.md)
- [Strategy-scoped permissions operational with ≥ 5 role templates](../objectives/strategy-scoped-permissions-operational-with-5-role-templates.md)

## Timeline
- **Start Date**: Not set
- **Target Date**: 2026-12-31

## Content
# Role-Aware Access & Audit Trails

## The Problem

Strategy is sensitive. Board-level discussions, risk assessments, assumption validations, and funding strategies shouldn't be visible to everyone in the organisation. But Stratafy currently operates with workspace-level access — if you're in the workspace, you see everything.

Enterprise customers (the segment where Stratafy can command $2K–$5K/mo) require granular access control and comprehensive audit trails. This isn't just a feature request — it's a procurement blocker. No enterprise will put their actual strategy into a system without RBAC and audit.

Generic AI infrastructure handles this with standard RBAC (read/write/admin) and SOC2-style audit logs. But strategic access control needs to be smarter: access should follow the strategy hierarchy, not just user roles.

## The Approach

Build a role-aware access and audit system that:

1. **Strategy-scoped permissions** — Access follows the strategy tree. A product lead gets full access to their functional strategy and everything beneath it (initiatives, objectives, risks) but read-only access to peer strategies and no access to board-level risk registers.

2. **Role-based views** — Different roles see different context. The CEO sees the full tree with executive summaries. Team leads see their branch with operational detail. Board members see curated strategy reviews with risk overlays.

3. **Comprehensive audit trails** — Every action logged: who viewed what, who changed what, who made which decision. Immutable audit log that satisfies SOC2 and enterprise compliance requirements.

4. **AI interaction governance** — Log which strategic context was provided to AI agents, what recommendations were generated, and which actions were taken. This is unique to AI-native strategy platforms and a significant differentiator.

## Technical Design

- Permission model: workspace → strategy tree → entity level. Permissions cascade down the tree by default, with override capability at any node.
- Role templates: pre-built role configurations (CEO, Strategy Lead, Team Lead, Board Member, Analyst) that map to sensible permission defaults
- Audit log: append-only event store capturing all entity interactions with full context (user, action, entity, timestamp, IP, session)
- AI audit: separate log for AI interactions capturing context provided, prompt used, response generated, and user action taken
- API enforcement: permissions checked at the MCP tool level — every tool call validates access before executing
- Export: audit logs exportable in formats compatible with SOC2, ISO27001, and enterprise compliance tooling

## Success Criteria

- Strategy-scoped permissions operational: users only see entities within their granted scope
- At least 5 pre-built role templates covering common organisational structures
- Complete audit trail for all entity operations with zero gaps
- AI interaction audit capturing context assembly, recommendations, and outcomes
- SOC2 Type II readiness for audit trail and access control components
- Zero impact on query performance from permission checks (< 10ms overhead per call)

## Dependencies

- Requires team and role definitions to be populated in workspaces (the `create_team`, `add_team_member` tools exist but adoption is low)
- Database-level row security policies for defence-in-depth
- Legal review of audit log retention policies across jurisdictions
- Enterprise customer input on specific compliance requirements (SOC2, ISO27001, GDPR)
- Must not break existing workspace access — migration path from "everyone sees everything" to scoped permissions
