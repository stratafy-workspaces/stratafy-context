---
id: 1597a2a6-e55c-406d-b89a-6031bceeabc9
type: insight
source: stratafy_chat
category: product
impactLevel: high
confidenceLevel: confirmed
status: synthesized
actionable: true
---

# Full strategy tree scan needs to be a single action, not 7 manual steps

## Summary
Running alignment scans on 7 strategies required 7 separate UI actions. For reports to work at scale, users need "Scan All & Generate Report" as a single action with progress tracking. Batch scanning is a prerequisite for report adoption.

## Description
To generate the STIR alignment report, we had to manually: (1) run 7 individual alignment scans one-by-one from the UI, (2) pull all 7 reviews via MCP, (3) manually synthesize patterns, (4) generate the report as a markdown file. This workflow should be one click: "Run Full Alignment Scan" → system scans entire strategy tree → auto-generates synthesis report. The batch scan capability (STR-101) is a prerequisite for the report feature to be usable by customers without an MCP-savvy operator. Also needed: a way to trigger scans programmatically via MCP (currently UI-only for individual scans), and async handling for 7+ sequential LLM calls that could take 30-60 seconds.

## Classification
- **Source**: stratafy chat
- **Category**: product
- **Impact**: high
- **Confidence**: confirmed
- **Status**: synthesized
- **Actionable**: Yes
- **Tags**: alignment-scan, product-insight, ux, batch-operations


