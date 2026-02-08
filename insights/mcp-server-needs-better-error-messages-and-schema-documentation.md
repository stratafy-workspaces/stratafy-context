---
id: 30b34633-82fc-444f-ae1e-c3019d643932
type: insight
source: stratafy_chat
category: product
impactLevel: high
confidenceLevel: confirmed
status: processed
actionable: true
lastUpdated: 2026-02-06T08:26:34.118018+00:00
---

# MCP server needs better error messages and schema documentation

## Summary
Five MCP usability issues: unclear length limits, undocumented enums, no initiative hierarchy, generic errors, no schema introspection. High friction for AI agent usage.

## Description
Issues encountered while using Stratafy MCP server in Claude conversation today:

**1. Description length constraint — no clear error message**
Hit `description_length_check` but didn't know the limit. Had to guess and trim.
Fix: Return helpful error like "Description exceeds 1500 char limit (you sent 2300)"

**2. Status enum values not documented**
Used `status: "planned"` — failed. Had to guess `"draft"` was valid.
Fix: Document valid enums in MCP tool schema

**3. No parent_initiative_id field**
Wanted to link child initiatives to parent. Had to hack with "Part of: X" in description.
Fix: Add `parent_initiative_id` to enable initiative hierarchies

**4. Generic "Database error" on strategy update**
Just got `Error: Database error` — no details on what failed.
Fix: Pass through actual constraint violation message

**5. No way to query valid enum values**
Have to guess/remember status, priority, initiative_type values.
Fix: Add to tool descriptions or create `get_schema` tool

**Severity:** Issues 1, 4 are high friction for AI agents using MCP. Makes autonomous operation harder when errors aren't actionable.

## Classification
- **Source**: stratafy chat
- **Category**: product
- **Impact**: high
- **Confidence**: confirmed
- **Status**: processed
- **Actionable**: Yes
- **Tags**: mcp, developer-experience, error-handling, schema, bug


