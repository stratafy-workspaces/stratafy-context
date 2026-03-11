---
id: db892907-2f19-4a2c-b812-948db2265cd3
type: initiative
status: draft
priority: medium
strategy: Product Architecture
completionPercentage: 0
---

# Document Tree — Hierarchical Knowledge Base

## Description
Build a hierarchical document tree with a separate document_tree_nodes table that organizes workspace documents into navigable sections (Legal, HR, Research, etc.). Sections are lightweight containers; documents are referenced by node, keeping the tree independent from document data. Documents retain existing entity linking (strategies, initiatives, etc.) for strategic context. MCP-first implementation with 8 tree tools + search tool. Frontend uses Nuxt UI UTree component that replaces the standard left-hand sidebar when in documents view. All documents are synced to xAI Collections API for semantic/hybrid search — on every create and update, document content is uploaded to a per-workspace collection, enabling intelligent document retrieval across the knowledge base.

## Parent Strategy
[Product Architecture](../strategy/product/product-architecture.md)

## Status & Progress
- **Status**: draft
- **Priority**: medium
- **Completion**: 0%

## Key Objectives
No objectives defined

## Timeline
- **Start Date**: Not set
- **Target Date**: Not set

## Content
## Data Model

```
document_tree_nodes
  id                uuid PK
  workspace_id      uuid FK → workspaces
  parent_id         uuid FK → document_tree_nodes (nullable, null = root level)
  node_type         enum: 'section' | 'document'
  document_id       uuid FK → documents (nullable, null for sections)
  label             text (required for sections, falls back to doc title for document nodes)
  icon              text (nullable, optional custom icon)
  position          integer (ordering among siblings)
  created_at
  updated_at
  deleted_at        (soft delete)

  UNIQUE(workspace_id, document_id) WHERE document_id IS NOT NULL
  -- Enforces single-placement initially, drop later for multi-placement

  UNIQUE(workspace_id, parent_id, position)
  -- Ensures clean sibling ordering
```

## Key Design Decisions

1. **Tree is separate from documents** — sections are lightweight (label, icon, position) and don't need versioning, content, or tags. Documents aren't cluttered with container-only entries.

2. **Two dimensions of organization** — Structural (where a document lives in the tree) is independent from Contextual (which strategies/initiatives a document links to via document_links). Same document can be in Legal > Contracts structurally but linked to Fundraising Playbook contextually.

3. **Single placement initially, multi-placement later** — UNIQUE constraint on document_id prevents a document appearing in multiple locations. Drop the constraint later if needed.

4. **Unplaced documents are OK** — documents can exist without being in the tree. An "unplaced" indicator helps users organize incrementally.

5. **Category migration path** — existing document categories (legal, fundraising, sales) can seed initial top-level sections automatically.

6. **Read-focused UI, MCP-first editing** — Documents are primarily created and updated through MCP (agents). The frontend renders markdown read-only with a basic textarea toggle for quick manual edits. No rich text editor, no toolbar, no slash commands. This reinforces the thesis that agents manage strategic content while humans review and approve. Avoids the editor rabbit hole (TipTap/ProseMirror/BlockNote) which would consume weeks with zero strategic value.

## Frontend Document View

**Read mode (default):** Rendered markdown with good typography. Support for headings, lists, tables, code blocks with syntax highlighting, links, images, and mermaid diagrams. Clean, readable presentation.

**Edit mode (toggle):** Raw markdown textarea. No WYSIWYG, no toolbar. Just the markdown source with a save button. This is for quick corrections, not primary authoring.

**Context panel:** Shows entity links (which strategies, initiatives, decisions this document connects to), document metadata (status, category, tags, version), and tree location.

**The primary creation and editing workflow is through MCP** — agents create documents, file them in the tree, and link them to the right entities. The UI is for reading, reviewing, and light edits.

## MCP Tools (Phase 1)

**Core tree operations:**
- `create_tree_node` — create a section or place a document. Params: parent_id, node_type, document_id (if document), label, icon, position
- `get_document_tree` — return full workspace tree (or subtree from a node), nested structure ready for UI
- `update_tree_node` — rename section, change icon, update position
- `move_tree_node` — move a node to a different parent/position, handles sibling reordering
- `delete_tree_node` — remove a node. Sections with children should fail or require force flag

**Convenience operations:**
- `place_document` — shorthand: put document_id under parent_id
- `unplace_document` — remove document from tree without archiving the document
- `get_unplaced_documents` — list documents not in any tree location

**Search operations:**
- `search_documents` — semantic/hybrid search across workspace documents via xAI Collections. Params: query, retrieval_mode (semantic|keyword|hybrid), limit

## Demo Moment: ScaleUp Case Study

At the end of the ScaleUp demo, demonstrate the complete document lifecycle in a single agent interaction:

**The prompt:** "Create a case study document based on our ScaleUp engagement so far. File it under Sales > Case Studies and link it to the ScaleUp Company Engagement strategy and the Advisory Firms initiative."

**What the agent does (visible in real-time):**
1. Calls `create_document` — generates a markdown case study pulling from the strategic context (ScaleUp strategy, objectives, engagement phases, outcomes)
2. Calls `create_tree_node` (or `place_document`) — files it under Sales > Case Studies in the document tree
3. Calls `add_document_link` — links to ScaleUp Company Engagement strategy
4. Calls `add_document_link` — links to Advisory Firms as Customer Segment initiative

**What ScaleUp sees:**
- A professionally structured case study appears in the document tree under the right section
- Opening it shows rendered markdown with their engagement story
- The context panel shows it's linked to their strategy and the advisory firms initiative
- The document is immediately searchable via semantic search

**Why this lands:**
- It demonstrates the full loop: strategy → execution → evidence → organized knowledge
- It shows documents aren't just files — they're strategically connected artifacts
- It proves the MCP-first model: one natural language instruction created, filed, and linked a document
- For an advisory firm, this is exactly what they'd want for every client engagement

## xAI Collections Integration — Embedding & Search

### Architecture

Each workspace gets a dedicated xAI Collection. Documents are synced to this collection as embeddings, enabling semantic search, keyword search, and hybrid retrieval across the entire knowledge base.

### How It Works

**On document create:** After persisting to the database, the document content (title + content markdown) is uploaded to the workspace's xAI Collection as a file. The xAI file_id is stored on the document record (new field: `xai_file_id`).

**On document update:** The existing file is removed from the collection and re-uploaded with the updated content. xAI handles re-indexing automatically. The new file_id replaces the old one.

**On document archive/delete:** The file is removed from the xAI Collection.

### Data Model Addition

```
documents table (add fields):
  xai_file_id       text (nullable) — the xAI file ID for this document in Collections
  xai_synced_at     timestamptz (nullable) — when last synced to Collections
```

```
workspaces table (add field):
  xai_collection_id text (nullable) — the xAI Collection ID for this workspace's documents
```

### xAI API Integration

**Collection setup (per workspace, lazy creation):**
```python
collection = client.collections.create(
    name=f"stratafy-docs-{workspace_id}",
)
```

**Document sync (on create/update):**
```python
# Remove old file if updating
if document.xai_file_id:
    client.collections.remove_document(collection_id, file_id)

# Upload current content
content = f"# {document.title}\n\n{document.content}".encode('utf-8')
uploaded = client.collections.upload_document(
    collection_id, name=f"{document.slug}.md", data=content
)
```

**Search (REST):**
```bash
curl -X POST https://api.x.ai/v1/documents/search \
  -H "Authorization: Bearer $XAI_API_KEY" \
  -d '{"query": "...", "source": {"collection_ids": ["..."]}, "retrieval_mode": {"type": "hybrid"}}'
```

### Pricing

- Search: $2.50 per 1,000 searches (negligible at current volumes)
- Storage/indexing: free tier available

### Sync Strategy

**Phase 1 (synchronous):** Upload inline during create/update. Adds ~1-2s latency. Acceptable initially.

**Phase 4 (async):** Background job/queue decouples write latency. Track via `xai_synced_at`.

### MCP Search Tool

```
search_documents
  query             string (required)
  retrieval_mode    enum: 'semantic' | 'keyword' | 'hybrid' (default: hybrid)
  limit             integer (default: 10, max: 50)

Returns: array of { document_id, title, slug, relevance_score, matched_content_snippet }
```

### Future: Grok Collections Search Tool

xAI supports Collections as a server-side tool within Grok completions. Stratafy agents could use Grok with `collections_search` for autonomous document-grounded reasoning.

## Frontend (Phase 2) — Nuxt UI Tree Sidebar

- Uses Nuxt UI `UTree` component (v4.4+)
- Replaces standard left-hand sidebar when in documents area
- Sections render with folder expand/collapse icons
- Documents render with file/status icons, clicking opens rendered markdown in main area
- Custom slots for status badges and action menus
- `get-key` uses node `id` for unique identification
- **Search bar at top** — queries xAI Collections, filters/highlights matching documents
- Route-based: `/documents/**` activates tree sidebar, back button returns to standard nav

## Sidebar Replacement Behavior

- Documents route activates tree sidebar mode
- Tree shows sections and documents hierarchically
- Clicking a document opens rendered markdown in main content area
- Breadcrumb at top for navigation context
- Toggle or back button to return to standard nav
- Mobile: tree via slide-over or drawer

## get_document_tree Response Shape

```json
[
  {
    "id": "node-uuid",
    "label": "Legal",
    "node_type": "section",
    "icon": "i-lucide-scale",
    "children": [
      {
        "id": "node-uuid-2",
        "label": "Founder Advisor Agreement",
        "node_type": "document",
        "document_id": "0ea9288c-...",
        "status": "draft"
      }
    ]
  }
]
```

## Position Management

Integer positions with gap strategy (10, 20, 30...) to allow insertions without reindexing.

## Implementation Phases

**Phase 1: Database + MCP + Embeddings (1.5 weeks)**
- Migration: document_tree_nodes table + xai fields on documents/workspaces
- Supabase RLS policies
- xAI Collections: workspace collection creation, document sync on create/update/delete
- All MCP tools including search_documents
- Seed existing docs into tree based on categories
- Backfill existing documents into xAI Collection
- Test the ScaleUp demo flow end-to-end via MCP

**Phase 2: Frontend — Read-focused Document View + Tree Sidebar (1 week)**
- Markdown renderer (rendered view with good typography, tables, code highlighting, mermaid)
- Basic textarea edit toggle for manual corrections
- Entity links / context panel
- UTree sidebar integration
- Search bar wired to xAI Collections

**Phase 3: Interactions (3-5 days)**
- Drag-and-drop reordering in tree
- Context menus (new section, place document, move)
- Unplaced documents panel

**Phase 4: Polish (ongoing)**
- Async embedding sync
- Search result highlighting in tree
- Keyboard navigation
- Multi-placement support
- Tree state persistence per user
- Grok collections_search for agent reasoning
