---
id: bedbf5b2-a7d7-4b91-a385-2a49546b7bf6
type: assumption
confidence: likely
assumptionType: technical
impactIfWrong: medium
status: active
---

# Sub-200ms context delivery matters for AI agent interactions

## Description
Users will abandon strategic AI that feels slow in conversational flow. If it takes 2-3 seconds for an AI agent to load strategic context before responding, people won't use Stratafy in the flow of work — they'll only use it for deliberate, scheduled sessions. The "strategy available wherever decisions happen" vision requires context to be instant. If wrong, users may tolerate latency for high-value strategic queries, and the caching investment can be deferred.

## Assessment
- **Confidence**: likely
- **Type**: technical
- **Impact if Wrong**: medium
- **Status**: active

## Validation
- **Method**: Measure current MCP response times for workspace_snapshot and strategy_tree calls. Survey users on perceived latency. Compare engagement rates for fast vs. slow context-loading sessions.
- **Validated At**: Not yet validated
- **Evidence**: No evidence recorded
