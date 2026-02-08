---
id: ee91c027-c47f-4a40-bea8-0b851d991fee
type: insight
source: stratafy_chat
category: operational
impactLevel: medium
confidenceLevel: confirmed
status: processed
actionable: true
lastUpdated: 2026-02-06T08:23:10.853225+00:00
---

# Meeting Prep Agent Design — Next-Day Prep with Calendar Write-Back

## Summary
Meeting Prep Agent designed with next-day prep (not same-day), calendar write-back (prep link in event), and data fusion from Attio + Stratafy + web. Second agent deployment, pattern is repeatable.

## Description
Deployed Meeting Prep Agent brief today. Key design decisions:

1. **Next-day prep, not same-day**: Agent runs at 6 PM, prepares for tomorrow. Leonard reviews in morning with 24+ hours lead time. No scrambling before calls.

2. **Calendar read AND write**: Agent reads tomorrow's meetings, but also WRITES the prep link back into the calendar event description. One click from meeting to context.

3. **Data fusion**: Pulls from Attio (contact, company, pipeline), Stratafy (strategies, insights), and web (recent news). Synthesizes into single brief.

4. **Linear as artifact store**: Briefs live as Linear issues, linked from calendar. Audit trail, reviewable, can add notes.

This is the second agent after Chief of Staff. Pattern is proving repeatable: define role, set heartbeat, connect data sources, deliver via Linear + Telegram.

## Classification
- **Source**: stratafy chat
- **Category**: operational
- **Impact**: medium
- **Confidence**: confirmed
- **Status**: processed
- **Actionable**: Yes
- **Tags**: agents, meeting-prep, automation, calendar, workflow


