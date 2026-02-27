---
id: ca33d4fd-de1d-4591-a12a-4dfbe47ea2e5
type: assumption
confidence: hypothesis
assumptionType: strategic
impactIfWrong: high
status: active
lastUpdated: 2026-02-27T16:55:41.817661+00:00
---

# Role-aware unified chat interface outperforms per-initiative workspace links

## Description
Evolved from the Aligned "single link per deal" pattern. Rather than giving users a link per strategic initiative (which fragments context), give each user a single role-aware chat interface that already knows their strategic context, operational tasks (via Linear integration), and agent activity. The system brings the relevant workspace to the user, filtered by role, rather than requiring the user to navigate to a workspace. This is the MCP architecture's natural expression: Linear provides operational layer, Stratafy provides strategic layer, role-aware context packaging stitches them together per user. If wrong — if users need explicit workspace boundaries to stay focused and avoid context overload — then per-initiative or per-team scoping may be necessary as a UX layer on top.

## Assessment
- **Confidence**: hypothesis
- **Type**: strategic
- **Impact if Wrong**: high
- **Status**: active

## Validation
- **Method**: Test with STIR: give team members a single chat interface with role-aware context spanning all 6 sub-strategies + their Linear tasks. Measure: do users feel oriented or overwhelmed? Do they naturally ask cross-initiative questions? Does strategic context improve task execution quality? Compare engagement depth vs a hypothetical per-initiative link approach. If users consistently narrow their own scope manually, the unified view may need optional focus modes.
- **Validated At**: Not yet validated
- **Evidence**: No evidence recorded
