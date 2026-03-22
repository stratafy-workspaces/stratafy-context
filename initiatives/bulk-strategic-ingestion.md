---
id: 9c9333b8-26e7-45db-ae84-d3be88f3f00d
type: initiative
status: draft
priority: medium
strategy: Strategic AI Infrastructure
completionPercentage: 0
---

# Bulk Strategic Ingestion

## Description
Deferred. Current ingestion path is Claude Cowork plugins (strategy-first-principles, strategic capture, workspace builder) which provide guided, human-in-the-loop workspace creation for smaller companies. The bulk automated pipeline (PDF/DOCX → extract → propose → review → commit) will evolve from this plugin foundation as customer scale demands it. The two-track governance model (direct write vs proposal pipeline) remains the architectural target — plugins are Track 1 today, bulk ingestion becomes Track 2 when enterprise customers need it.

## Parent Strategy
[Strategic AI Infrastructure](../strategy/product/strategic-ai-infrastructure.md)

## Status & Progress
- **Status**: draft
- **Priority**: medium
- **Completion**: 0%

## Key Objectives
- [Entity extraction accuracy ≥ 85% against human-classified test set](../objectives/entity-extraction-accuracy-85-against-human-classified-test-set.md)
- [20-page strategy PDF ingested into structured workspace in under 5 minutes](../objectives/20-page-strategy-pdf-ingested-into-structured-workspace-in-under-5-minutes.md)

## Timeline
- **Start Date**: Not set
- **Target Date**: 2026-06-30

## Content
# Bulk Strategic Ingestion

## The Problem

Getting strategic content into Stratafy today is manual: users create entities one by one through the UI or MCP tools. This creates a cold-start problem — new workspaces feel empty, and migrating from existing tools (Google Docs strategy decks, Notion boards, spreadsheet OKRs, PDF strategic plans) requires significant manual effort.

Generic AI infrastructure solves ingestion with chunking pipelines that split documents into embeddings. But chunking a strategy document into flat vectors destroys the very structure that makes it strategic — the hierarchy, the links between objectives and initiatives, the distinction between a belief and a principle.

Beyond the technical parsing challenge, there's a governance dimension: **not all ingestion should land directly in the strategy**. Some users and agents are trusted to write directly. Others — external sources, AI agents scanning the market, junior team members — should propose changes that go through a review pipeline before affecting the strategy tree.

## Two-Track Ingestion Model

### Track 1: Direct Write
Trusted users and authorised agents who can create, update, and delete strategy entities directly via MCP tools or the UI. This is the current model and remains appropriate for:
- Workspace admins and strategy owners
- AI agents operating within tightly scoped, pre-approved workflows
- Authenticated integrations with verified data sources

### Track 2: Proposal Pipeline
Users, agents, or external sources that submit proposed changes which must pass through review and approval before affecting the strategy. This applies to:
- **Bulk document imports** — A PDF parsed into *proposed* entities, staged for human review before committing to the workspace
- **AI agent recommendations** — Market signals, radar findings, and strategic suggestions proposed as changes to the strategy tree
- **Team member suggestions** — A product manager proposing a new initiative, or a team lead suggesting an assumption needs updating
- **Cross-workspace inputs** — Insights from one workspace proposed as relevant to another
- **External integrations** — Data from CRM, analytics, or financial tools proposed as metric updates or new signals

### Proposal Pipeline Architecture
The proposal pipeline requires:
1. **Staging area** — Proposed entities stored separately from the live strategy tree, with full metadata (source, proposer, confidence, rationale)
2. **Strategy diff view** — Visual comparison showing what would change in the strategy tree if proposals are accepted
3. **Review workflow** — Assign reviewers, add comments, approve/reject/request-changes (similar to code review)
4. **Partial acceptance** — Accept 3 of 5 proposed entities from a bulk import, reject the rest
5. **Audit trail** — Who proposed what, who reviewed, who approved, when it landed in the strategy
6. **Batch operations** — Accept/reject multiple proposals at once, especially for bulk imports

## The Approach

Build a schema-aware strategic extraction pipeline with governance:

1. **Accepts bulk input** — Upload strategy documents (PDF, DOCX, PPTX), paste content, or connect to external sources (Google Docs, Notion, Linear)
2. **Extracts strategic entities** — Use LLM-powered extraction to identify missions, visions, values, strategies, initiatives, objectives, metrics, risks, and assumptions from unstructured content
3. **Preserves structure** — Map extracted entities to Stratafy's schema, inferring hierarchy and relationships
4. **Routes to correct track** — Based on the source and user permissions, extracted entities either commit directly (Track 1) or enter the proposal pipeline (Track 2)
5. **Presents for review** — Proposed entities shown to reviewers with confidence scores, source attribution, and strategy diff preview
6. **Commits on approval** — Approved proposals land in the strategy tree with full provenance metadata

## Technical Design

- Document processing pipeline: PDF/DOCX/PPTX → text extraction → LLM entity extraction → schema mapping → routing decision → direct commit or proposal staging
- Extraction prompt engineering: fine-tuned prompts for each entity type, with examples from the strategy-first-principles framework
- Proposal data model: `proposals` table with status (pending/approved/rejected/partial), linked entities, reviewer assignments, and comments
- Routing rules engine: permission-based routing that determines direct-write vs. proposal based on user role, source type, and entity sensitivity
- Batch MCP operations: new bulk-create endpoints that accept arrays of entities with relationship metadata
- Confidence scoring: each extracted entity gets a confidence score; low-confidence items always routed to proposal pipeline regardless of user permissions
- Notification system: reviewers notified of pending proposals, proposers notified of decisions

## Success Criteria

- A 20-page strategy PDF can be ingested into proposals in under 5 minutes, with review and commit adding minimal overhead
- Entity extraction accuracy ≥ 85% (measured against human-classified test set)
- Proposal pipeline supports full review workflow: assign, comment, approve, reject, partial accept
- Strategy diff view clearly shows impact of accepting proposals on the existing strategy tree
- Reduces workspace setup time from days to hours for new customers
- Supports at least PDF, DOCX, PPTX, and plain text on launch
- Clear audit trail from source document → extracted proposal → review decision → committed entity

## Dependencies

- Requires robust document parsing (pdf-parse, mammoth, pptx libraries)
- LLM extraction quality depends on prompt engineering and model capability
- Needs the strategy-first-principles schema as the extraction target
- Proposal data model and review UI design
- **Role-Aware Access & Audit Trails initiative** — routing rules depend on role definitions and permissions being in place
- **Strategic Engagement Analytics initiative** — proposal acceptance rates and review times are key engagement metrics
