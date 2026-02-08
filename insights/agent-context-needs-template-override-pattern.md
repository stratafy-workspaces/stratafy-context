---
id: bc4b7edf-e757-4f8d-9463-395d63dccdfb
type: insight
source: stratafy_chat
category: product
impactLevel: medium
confidenceLevel: confirmed
status: processed
actionable: true
lastUpdated: 2026-02-06T08:22:43.988967+00:00
---

# Agent context needs template + override pattern

## Summary
Agents should support: base template for consistency, plus agent-specific override for customization. Override modes: append, prepend, or replace.

## Description
When registering an agent, rigid template-only approach limits flexibility. Real use cases need customization: Chief of Staff needs founder template PLUS "coordinate through Linear, escalate to Telegram". Solution: prompt_template_id (nullable) + prompt_override (text) + override_mode (append|prepend|replace). Agents can use template only, override only, or both combined.

## Classification
- **Source**: stratafy chat
- **Category**: product
- **Impact**: medium
- **Confidence**: confirmed
- **Status**: processed
- **Actionable**: Yes
- **Tags**: agent-registry, context-packaging, flexibility, design-pattern


