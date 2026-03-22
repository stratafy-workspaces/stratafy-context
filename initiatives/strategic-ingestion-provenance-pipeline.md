---
id: 7241e50b-467f-4524-8b75-c40f9a86a38a
type: initiative
status: in_progress
priority: high
strategy: Strategic AI Infrastructure
completionPercentage: 95
---

# Strategic Ingestion & Provenance Pipeline

## Description
Provenance-aware mutation pipeline built into the MCP middleware layer. Every MCP mutation is tracked with full causal chain: plugin, command, reasoning, user, entity. All phases complete except governance gates (Phase 2, deferred). Phase 1: fire-and-forget tracking on ~80 mutation tools, 168+ tests. Phase 3: all 11 plugin prompts updated across 22 files. Phase 4: provenance UI at /provenance + History tab on strategy detail pages with versions grouped with nested provenance. Enhanced fields computed server-side: change_magnitude, evidence_type, confidence_score. LLM reason/intent captured. Daily snapshot versions enriched with provenance_summary and LLM-assessed ai_assessment. Content escaping fix applied globally.

## Parent Strategy
[Strategic AI Infrastructure](../strategy/product/strategic-ai-infrastructure.md)

## Status & Progress
- **Status**: in progress
- **Priority**: high
- **Completion**: 95%

## Key Objectives
No objectives defined

## Timeline
- **Start Date**: Not set
- **Target Date**: Not set

## Content
# Strategic Ingestion & Provenance Pipeline

## The Insight

The Stratafy Team is 11 executive plugins, all connected to the workspace via MCP. Today, every plugin has full read/write access with no provenance tracking. The link between "why this change happened" and "what changed" exists only in conversation context, lost after the session ends.

The solution: make every mutation provenance-aware at the middleware level. Same tools, same endpoint — but every change carries its full lineage. Governance (proposal vs auto-commit) is determined by the caller's workspace role, not the plugin type.

## Core Design Principles

1. **Provenance is always captured** — whether auto-committed or queued, every mutation has a trail
2. **Governance is role-based, not plugin-based** — the same FD plugin auto-commits for an owner but creates proposals for a member
3. **One MCP endpoint** — no split. The auth token carries the user's workspace role. Middleware handles the rest.
4. **Plugin authors don't think about governance** — they just pass provenance context on mutations. The system decides.
5. **Zero friction for solo founders** — they're the owner, everything auto-commits
6. **Provenance is not just a log** — it's the living proof that strategy is still valid, intentionally maintained, and defensible

## The Eight Non-Negotiables of Provenance

| Element | What Stratafy Captures | Where |
|---|---|---|
| **Who** | `performed_by` (user ID → full name + role resolved in API) | provenance_records |
| **When** | `performed_at` (log time) + `effective_at` (when change takes effect) | provenance_records |
| **What changed** | `field_changes` JSONB diff (old → new per field) | provenance_records |
| **Why** | `change_reasoning` (mandatory short reason) | provenance_records |
| **Source of truth** | `source_ref` (URL, signal ID, or description) + `source_plugin` | provenance_records |
| **Approval chain** | `approval_mode` + `reviewed_by` + `review_notes` | provenance_records |
| **Versioning** | `change_magnitude` labels (minor / major / pivot) | provenance_records |
| **Confidence / Impact** | `confidence_score` (0–100) + `evidence_type` | provenance_records |

Plus a ninth capability not in typical provenance systems: **validity reaffirmation** — a lightweight signal that strategy is still intentional, not just untouched.

## Architecture

### How It Works

Every mutation tool already accepts `_intent` and `_reason` parameters. We extend this pattern with provenance fields and wrap every mutation in middleware.

#### Layer 1: Tool Parameters (what the plugin provides)

Every mutation tool call includes provenance context:

```
update_strategy(
  id: "strategy-uuid",
  description: "new description",

  // Already exists
  _intent: "autonomous",
  _reason: "Financial scan detected misalignment",

  // Core provenance fields
  _source_plugin: "stratafy-fd",
  _source_command: "financial-alignment-scan",
  _source_ref: "signal-uuid or article URL",
  _change_reasoning: "40% of spend has no strategic mapping...",

  // Enhanced provenance fields
  _change_magnitude: "major",          // minor | major | pivot
  _confidence_score: 72,               // 0-100
  _evidence_type: "financial",         // data | customer_feedback | market_signal | intuition | financial
  _effective_at: "2026-04-01"          // when this change takes effect (defaults to now)
)
```

The plugin commands (markdown files) instruct Claude to always pass these fields. The tools themselves don't change — they just accept optional provenance metadata.

#### Layer 2: Backend Middleware (what the system does)

Every mutation tool passes through a provenance middleware before hitting the database:

```
Request comes in
  → Identify caller (user ID, workspace role from auth token)
  → Snapshot "before" state of the entity
  → Check workspace role:
      Owner/Admin → execute mutation directly
      Member → create proposal instead, return proposal ID
  → Capture "after" state (or proposed state)
  → Write provenance record (including magnitude, confidence, effective_at)
  → Return result (or proposal confirmation)
```

The middleware is transparent. `update_strategy` is still `update_strategy`. Existing code doesn't break.

#### Layer 3: Proposal & Reaffirmation Tools (Guardian additions)

New tools, available to Guardian-authorized users (owner/admin/coach):

| Tool | Purpose |
|------|---------|
| `list_proposals` | Pending proposals, filterable by plugin, status, date |
| `review_proposal` | Accept / modify / reject a single proposal with notes |
| `batch_review_proposals` | Bulk accept/reject for low-risk proposals |
| `get_provenance` | Full provenance chain for any entity |
| `get_provenance_stats` | Ingestion intelligence — acceptance rates, source analysis, confidence distribution |
| `reaffirm_entity` | Log that an entity was reviewed and is still intentionally valid (no change needed) |
| `list_stale_entities` | Surfaces entities that haven't been changed or reaffirmed in N days |

#### Layer 4: Plugin Commands (what changes in markdown)

Each plugin's CLAUDE.md gets a provenance section:

```markdown
## Provenance

On every mutation tool call, always include:
- `_source_plugin`: "stratafy-fd"
- `_source_command`: the command being run
- `_change_reasoning`: 1-2 sentences explaining WHY this change is needed
- `_change_magnitude`: "minor" (wording/detail), "major" (scope change), or "pivot" (direction change)
- `_confidence_score`: 0-100 based on evidence quality
- `_evidence_type`: one of data | customer_feedback | market_signal | intuition | financial
- `_effective_at`: when the change takes effect (omit if immediate)

The system handles approval automatically based on the user's workspace role.
If changes are queued as proposals, tell the user they've been submitted for review.
```

### Role-Based Governance

| Workspace role | Mutation behaviour | Provenance |
|---------------|-------------------|------------|
| **Owner** | Auto-commit | Full provenance logged |
| **Admin** | Auto-commit | Full provenance logged |
| **Member** | Proposal created → queued for review | Full provenance logged |
| **Viewer** | Read only | N/A |

The same `update_strategy` call behaves differently based on who's calling. The plugin doesn't know or care.

### Plugin Access Matrix

| Plugin | Stratafy MCP | Linear | Gmail | Calendar | Slack | Notion |
|--------|-------------|--------|-------|----------|-------|--------|
| **Guardian** | Full R/W + review tools | Yes | Yes | Yes | Yes | Yes |
| **FD** | R/W (role-gated) | Yes | - | - | - | - |
| **Team** | R/W (role-gated)* | Yes | - | - | - | - |
| **CoS** | R/W (role-gated) | Yes | - | Yes | - | - |
| **CMO** | R/W (role-gated) | Yes | Yes | - | - | - |
| **CRO** | R/W (role-gated) | Yes | Yes | - | - | - |
| **CPO** | R/W (role-gated) | Yes | - | - | - | - |
| **CTO** | R/W (role-gated) | Yes | - | - | - | - |
| **CHRO** | R/W (role-gated) | Yes | - | - | - | - |
| **GC** | R/W (role-gated) | Yes | - | - | - | - |
| **Advisor** | R/W (role-gated) | - | - | - | - | - |

*Team plugin's lightweight writes (log_activity, record_metric_value, log_bug, capture) are never gated.

### Lightweight Write Exceptions

Not every write needs provenance or governance. Data entry operations are never gated:

| Tool | Provenance | Governance gate | Why |
|------|-----------|----------------|-----|
| `log_activity` | No | Never | Activity logging — tracking, not strategic mutation |
| `record_metric_value` | No | Never | Data point entry — objective measurement |
| `log_bug` | No | Never | Feedback capture — not strategic content |
| `capture` (Team) | Lightweight | Never | Quick insight/signal capture from conversations |
| All other mutations | Full | Role-based | Strategic content that shapes the workspace |

**The line: if it changes the strategy tree, it gets provenance and role-based governance. If it records data about the world, it writes directly.**

## Database Schema

```sql
create table provenance_records (
  id uuid primary key default gen_random_uuid(),
  workspace_id uuid not null references workspaces,

  -- What changed
  entity_type text not null,
  entity_id uuid not null,
  action text not null,          -- create, update, delete, link, unlink, reaffirm
  field_changes jsonb,           -- { field: { from, to } }

  -- Who and why
  source_plugin text,            -- stratafy-fd, stratafy-cmo, etc.
  source_command text,           -- financial-alignment-scan, brand-audit, etc.
  source_ref text,               -- URL, signal_id, or description of trigger
  change_reasoning text,         -- why this change was proposed/made

  -- Change characterisation (enhanced)
  change_magnitude text,         -- 'minor' | 'major' | 'pivot'
  confidence_score smallint,     -- 0-100 (how data-backed was this change?)
  evidence_type text,            -- 'data' | 'customer_feedback' | 'market_signal' | 'intuition' | 'financial'
  effective_at timestamptz,      -- when the change takes effect (defaults to performed_at if null)

  -- Who acted
  performed_by uuid not null references users,
  performed_at timestamptz not null default now(),

  -- Approval
  approval_mode text not null,   -- auto (owner/admin) or reviewed (member proposal)
  status text not null default 'committed',  -- committed, pending, modified, rejected
  proposed_state jsonb,          -- what was proposed (for pending/modified)
  reviewed_by uuid references users,
  reviewed_at timestamptz,
  review_notes text
);

-- Indexes
create index idx_provenance_workspace on provenance_records(workspace_id);
create index idx_provenance_entity on provenance_records(entity_type, entity_id);
create index idx_provenance_status on provenance_records(workspace_id, status) where status = 'pending';
create index idx_provenance_plugin on provenance_records(source_plugin);
create index idx_provenance_magnitude on provenance_records(workspace_id, change_magnitude);
create index idx_provenance_effective on provenance_records(workspace_id, effective_at);
```

### The `reaffirm` Action

The `reaffirm` action type on `provenance_records.action` records intentional validity reviews without a content change. Used by `reaffirm_entity` tool (Guardian only):

- No `field_changes` (nothing changed)
- `change_reasoning` captures the review outcome ("Still valid — cost reduction mandate unchanged despite Q1 miss")
- `confidence_score` can be updated independently of content
- Enables staleness detection: any entity not changed or reaffirmed in N days surfaces as potentially stale

This closes the "drift detection" loop — the system can distinguish between "unchanged because still valid" and "unchanged because nobody has looked at it."

## What This Enables

### Traceability View

On any entity page, a user can see: "This strategy was last updated on 12 March. The change originated from a McKinsey article on AI infrastructure spending, captured via the CMO's brand-audit command, which surfaced the insight that the market is rewarding infrastructure investment over efficiency. Change magnitude: major. Confidence: 78% (market signal). Leonard auto-approved (workspace owner). Effective from Q2 2026."

### Ingestion Intelligence

- Which executives generate the most changes? (activity signal)
- In governed workspaces: acceptance rate by plugin, by source type? (quality signal)
- What does the Guardian modify before accepting? (gap signal)
- Which source types (articles, conversations, data) drive the most strategic change?
- Which parts of the strategy are most actively informed by external intelligence?
- What is the average confidence score by plugin / by evidence type? (quality of input signal)
- Which pivot-magnitude changes had the lowest confidence scores? (risk signal)
- What percentage of strategies have been reaffirmed in the last 90 days? (health signal)

### Staleness Detection

Guardian's `list_stale_entities` surfaces strategy elements that haven't been touched or reaffirmed within a configurable window (default: 90 days). The distinction between "stale" and "stable" is made by the reaffirmation record — silence alone is not a signal of validity.

### Audit & Governance

- Full trail from external content to workspace change
- Every change has provenance — even auto-committed ones
- Proposal history preserved even for rejected changes (strategic learning)
- Compliance-ready — any auditor can trace any change, its magnitude, and the confidence behind it
- `effective_at` enables accurate time-travel: "reconstruct the strategy as it was *in effect* on date X" (not just the latest logged state)

### Coach/CSIO Weekly Rhythm (governed workspaces)

1. Executive plugins run their commands during the week
2. Members' proposals accumulate in the queue
3. Coach/CSIO reviews proposals via Guardian every Friday
4. Accepted changes flow into the workspace
5. Rejected proposals become learning signals
6. Guardian's weekly reaffirmation sweep flags anything approaching staleness

### Solo Founder Daily Flow (direct workspaces)

1. Founder runs any executive plugin
2. Changes auto-commit immediately — zero friction
3. Full provenance captured in background (with magnitude, confidence, effective date)
4. Founder can review their own change history anytime via Guardian
5. If they bring on team members later, governance activates automatically for those members
6. Quarterly, founder uses `list_stale_entities` to reaffirm or update anything that's drifted

## Relationship to Other Initiatives

- **Bulk Strategic Ingestion** (deferred): Will sit on top of this pipeline as another mutation source when enterprise scale demands it
- **Strategic Evolution & Time-Travel**: Provenance data enriches snapshot narratives and causal chain detection; `effective_at` enables accurate strategy reconstruction at any point in time; `change_magnitude` enriches AI narrative summaries ("three minor updates and one pivot in Q1")
- **Role-Aware Access & Audit Trails**: Provenance records form the foundation of decision audit trails
- **The Stratafy Team strategy**: Provenance makes every executive's contribution visible, traceable, and scored

## Execution Approach

### Phase 1: Provenance Middleware ✅
1. Create `provenance_records` table
2. Build provenance middleware that wraps mutation tools
3. Add `_source_plugin`, `_source_command`, `_source_ref`, `_change_reasoning` as optional parameters to all mutation tools
4. Auto-commit with provenance logging for all users (governance comes in Phase 2)

### Phase 2: Role-Based Governance (deferred — team workspaces)
5. Add workspace role check to provenance middleware
6. Implement proposal creation for member-role mutations
7. Add Guardian-only tools: `list_proposals`, `review_proposal`, `batch_review_proposals`
8. Add `/review-proposals` command to Guardian plugin

### Phase 3: Plugin Provenance Context ✅
9. Update each plugin's CLAUDE.md with provenance section
10. Update plugin commands to pass provenance fields on mutations
11. Update role-specific external MCP access (Gmail for CMO/CRO, Calendar for CoS)

### Phase 4: Provenance UI & Intelligence ✅
12. Build provenance view on entity pages (trace any change to source)
13. Build `get_provenance` and `get_provenance_stats` tools
14. Connect provenance data to time-travel snapshot narratives

### Phase 5: Enhanced Provenance (new — next sprint)
15. Add `change_magnitude`, `confidence_score`, `evidence_type`, `effective_at` columns to `provenance_records`
16. Update all mutation tools to accept enhanced provenance parameters
17. Update all 11 plugin CLAUDE.md files with enhanced provenance instructions
18. Add `reaffirm` action type + `reaffirm_entity` Guardian tool
19. Build `list_stale_entities` tool with configurable staleness window
20. Update `get_provenance` response to resolve `performed_by` to full name + workspace role (not just UUID)
21. Update time-travel queries to use `effective_at` for accurate historical reconstruction

