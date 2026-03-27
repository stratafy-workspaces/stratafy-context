---
id: 2b5f35f8-bb57-451d-ba3f-9d0cb2b02e02
type: initiative
status: active
priority: high
strategy: Core Product Capabilities
completionPercentage: 0
---

# Strategic Actions — Lightweight Task Assignment

## Description
Introduce a new 'Action' entity to Stratafy that enables lightweight, context-rich task assignment between users, experts, and agents. Actions carry strategic provenance — they link to the entities that triggered them (signals, assumptions, risks, decisions, causal chains, reviews) and provide enough background for the assignee to act independently and asynchronously.

## Parent Strategy
[Core Product Capabilities](../strategy/product/core-product-capabilities.md)

## Status & Progress
- **Status**: active
- **Priority**: high
- **Completion**: 0%

## Key Objectives
No objectives defined

## Timeline
- **Start Date**: Not set
- **Target Date**: Not set

## Content
# Strategic Actions — Design Overview

## What It Is
A lightweight Action entity that enables strategic task assignment between participants in the Stratafy ecosystem — users, Stratafy experts, and (later) autonomous agents.

## Core Design Principles
- **Not project management** — no subtasks, dependencies, Gantt charts, or sprint boards
- **Context-rich** — every action carries its strategic provenance (why it exists, what triggered it, what entities it relates to)
- **Async-first** — assignees can act on actions independently without needing to be in the originating session
- **Proposed-first** — actions start in a proposed state; a human must review and approve before they become active

## Action Entity Schema (v1)

### Core Fields
- `id` — unique identifier
- `name` — short action title
- `description` — what needs to be done
- `reason` — why this action exists, with strategic context
- `status` — proposed | open | in_progress | done | dismissed
- `priority` — low | medium | high | critical
- `assigned_to_type` — expert (v1), later: user, agent
- `assigned_to_id` — reference to the expert entity
- `created_by_type` — user (v1), later: expert, agent, system
- `created_by_id` — who or what created the action
- `due_date` — optional target date
- `workspace_id` — workspace scope

### Lifecycle Fields
- `dismissed_reason` — free-text explanation when status moves to dismissed (required on dismissal). Critical for tuning auto-generation quality in Phase 2.
- `completed_at` — timestamp when status moves to done. Enables cycle time measurement (proposed → done).

### Audit Fields
- `created_at` — timestamp
- `updated_at` — timestamp, auto-updated on every change
- `updated_by` — who or what made the last update

### Linking Fields
- `linked_entity` — single entity reference (Phase 1), expanding to array in Phase 2:
  - `entity_type` — strategy | signal | assumption | risk | decision | initiative | objective | insight | review | causal_chain
  - `entity_id` — reference ID
  - `link_role` — trigger | context | target

### Origin Tracking
- `origin_type` — session | signal | review | alert | causal_chain | manual
- `origin_ref` — reference to the originating event

## State Machine

```
proposed → open → in_progress → done
   ↓
   dismissed (requires dismissed_reason)
```

- **proposed** — awaiting human review
- **open** — approved and ready for the assignee
- **in_progress** — assignee is working on it
- **done** — completed (sets completed_at)
- **dismissed** — deemed unnecessary (dismissed_reason required)

## Phased Rollout

### Phase 1 (This Initiative) — Prove the Entity Model
Goal: Ship the smallest useful action loop as fast as possible.

1. Manual creation by users in sessions (Cowork, CLI)
2. Assigned to Stratafy experts (CTO, FD, CSIO, etc.)
3. All actions start as "proposed"
4. **Single-entity linking** — one linked entity per action (keeps UX simple)
5. Reason/background field with entity reference
6. `dismissed_reason` and `completed_at` captured from day one

### Phase 2 — Auto-generation & Multi-entity Linking
- Auto-generation from strategy reviews, causal chain alerts, assumption invalidations
- **Multi-entity linking** — expand to array of linked entities with roles
- Experts and agents can propose actions
- "My Actions" view per expert with full context
- Action digest in workspace pulse/health checks
- Dismissal analytics to tune auto-generation quality

### Phase 3 — Completion Triggers & Templates
- Action completion triggers (updates linked assumptions, closes risks)
- Action templates for recurring strategic rhythms
- Cross-workspace action coordination

