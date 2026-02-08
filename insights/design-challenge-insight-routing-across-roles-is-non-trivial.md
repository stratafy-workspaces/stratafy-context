---
id: c433af01-709b-467e-8d22-9775e747496c
type: insight
source: stratafy_chat
category: operational
impactLevel: high
confidenceLevel: likely
status: pending
actionable: true
lastUpdated: 2026-01-27T21:14:41.675867+00:00
---

# Design challenge: Insight routing across roles is non-trivial

## Summary
When an IC or Manager captures an insight, where does it go? Routing logic is hard: escalation triggers, visibility rules, originator feedback. Get this wrong and the system feels opaque or noisy.

## Description
When Manager captures insight suggesting strategy should change, routing logic is non-trivial: Does it go to CEO automatically? Sit in a queue? Does the Manager know it was captured? Wrong routing creates opacity (insights disappear) or noise (CEO drowns in IC feedback). Need clear design: (1) What triggers escalation? (2) Who sees what insights? (3) How does originator get feedback that their input was received/acted on? This is a hard design problem that will determine whether the feedback loop actually works.

## Classification
- **Source**: stratafy chat
- **Category**: operational
- **Impact**: high
- **Confidence**: likely
- **Status**: pending
- **Actionable**: Yes
- **Tags**: design, routing, insights, architecture, open-question


