---
id: c44c316b-4257-4d28-aade-c1b0d3e1b36b
type: decision
decisionType: type_2_reversible
status: decided
lastUpdated: 2026-01-30T12:33:15.250349+00:00
---

# Switch AI Tools Directory to ISR, Keep Blog Prerendered

## Description
Evaluate whether to change the blog and AI tools directory from pre-rendered (SSG) to Incremental Static Regeneration (ISR) to reduce build times as content scales.

## Details
- **Type**: Type 2 (Reversible)
- **Status**: decided
- **Authority**: Technical Director
- **Deadline**: No deadline
- **Decided At**: Not yet decided

## Context
AI Tools Directory: 1 tool published (ClawdBot), 3 more planned by Feb 15. Blog: 13 posts. Total site pages: 24. Build time: ~45s. Phase 1 target is 4 tools, Phase 2 envisions scaling to 100-500+ tools. ISR decision enables rapid directory expansion without deploy friction while preserving SEO-critical prerendering for blog content.

## Research
No research recorded

## Decision
Implement phased approach: Switch AI Tools to ISR (isr: 86400 for index, isr: true for individual pages), keep Blog prerendered until 50+ posts.

## Rationale
1. Current scale (24 pages) doesn't justify full ISR - prerendering isn't the bottleneck. 2. AI Tools is a directory play expected to scale to 100-500+ tools - ISR enables rapid expansion without deploy friction. 3. Blog SEO is critical at 13 posts - keep prerendered for instant static delivery to crawlers. 4. Reversible decision - can switch blog to ISR when triggers are met (50+ posts, 3x/week deploys, 5+ min builds).

## Outcome
No outcome recorded yet
