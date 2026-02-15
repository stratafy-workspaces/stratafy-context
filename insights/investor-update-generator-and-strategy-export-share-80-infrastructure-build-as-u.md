---
id: 98cb024b-da23-4b4a-be16-d8f6fc4e95eb
type: insight
source: stratafy_chat
category: product
impactLevel: medium
confidenceLevel: confirmed
status: pending
actionable: true
lastUpdated: 2026-02-08T22:16:59.001113+00:00
---

# Investor Update Generator and Strategy Export share 80% infrastructure — build as unified document generation engine

## Summary
Both initiatives pull from the same workspace data and apply different templates. Build a generic document generation engine with template types rather than two separate features.

## Description
The Investor Update Generator and Strategy Export to PDF initiatives share roughly 80% of their infrastructure: workspace snapshot → structured data extraction → template application → formatted output. Building one makes the other incremental. This suggests a generic 'workspace document generation' engine rather than two separate features. The engine takes a template type (investor update, strategy one-pager, board pack, alignment report) and applies the appropriate structure to the same underlying data pull. Implementation priority: build the shared engine with investor update as the first template, then add PDF export templates incrementally.

## Classification
- **Source**: stratafy chat
- **Category**: product
- **Impact**: medium
- **Confidence**: confirmed
- **Status**: pending
- **Actionable**: Yes
- **Tags**: architecture, investor-update, strategy-export, document-generation


