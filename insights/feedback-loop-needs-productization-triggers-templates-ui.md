---
id: 676cce45-a585-4253-b6dc-d9b5e04c2410
type: insight
source: stratafy_chat
category: operational
impactLevel: high
confidenceLevel: likely
status: pending
actionable: true
lastUpdated: 2026-01-27T00:22:33.735526+00:00
---

# Feedback loop needs productization — triggers, templates, UI

## Summary
Current loop is manual via Claude. To be a product: automated triggers, templated analysis prompts, one-click execution, approval flow, review history. This is Alignment Scan for insights.

## Description
The feedback loop that just ran was manual — I asked Claude to run it. For this to be a real product feature, it needs:

1. **Automated triggers**
   - Threshold: "You have 5+ pending insights. Review now?"
   - Time-based: "Weekly review scheduled for Monday 9am"
   - Event-based: "Major milestone completed. Time to recalibrate?"

2. **Templated analysis prompt**
   - Currently lives in Claude's reasoning
   - Needs to be a stored, versioned prompt template
   - Customizable per workspace or user

3. **One-click execution**
   - "Run Strategic Review" button
   - Shows recommendations in UI
   - Approve/modify/reject flow
   - Applies changes automatically

4. **Review history**
   - Log of all reviews run
   - What changed and why
   - Audit trail for governance

This is the Alignment Scan equivalent for insights → strategy, not just foundation → strategy.

## Classification
- **Source**: stratafy chat
- **Category**: operational
- **Impact**: high
- **Confidence**: likely
- **Status**: pending
- **Actionable**: Yes
- **Tags**: feedback-loop, product-roadmap, automation, feature-spec


