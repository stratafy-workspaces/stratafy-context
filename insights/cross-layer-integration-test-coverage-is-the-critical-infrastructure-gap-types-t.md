---
id: 921cc20e-86ab-4600-88d0-5cd2cfd3620b
type: insight
source: architecture_review
category: technology
impactLevel: high
confidenceLevel: confirmed
status: pending
actionable: true
---

# Cross-layer integration test coverage is the critical infrastructure gap — types trail implementation in 7 of 8 weeks

## Summary
TypeScript batch-fix commits (50-98 errors at a time) appeared in 7 of 8 weeks. Pre-push tests run in under 1 second. CI targeting main with unit tests only shipped in week 8. With 20+ layers and 169+ MCP tools, the regression surface area is large. The gap isn't unit tests — it's integration tests that exercise cross-layer flows (signal → insight → decision → initiative). This should be prioritised before the next expansion wave.

## Description
## Maps To
- **Strategic AI Infrastructure** — infrastructure quality concern
- **Product Architecture** — cross-cutting concern across all sub-strategies

## Evidence from Dev Reports
- Week 2: 27 TypeScript fixes + 276 ESLint warnings in dedicated commits
- Week 5: "resolve 98 lint and type errors in single pass", disabled typedPages to prevent TS2321 deep instantiation
- Week 6: "resolve 98 TypeScript errors across mcp, organogram, and metric layers"
- Week 7: ESLint/TS error resolution in 3 separate commits
- Week 8: CI targeting main only shipped this week

## Recommendation
Build integration tests for the critical cross-layer flows before the next expansion wave: (1) signal → insight synthesis pipeline, (2) distillation → health scoring → coaching prompt context, (3) MCP mutation → provenance capture → time-travel snapshot, (4) entity creation → embedding → semantic search retrieval. These are the flows where regressions would break the platform's core value proposition.

## The Pattern
The "ship features, then fix 50-98 type errors in a batch" pattern suggests the type system is trailing implementation rather than guarding it. Stricter CI gates earlier would have caught many of these.

## Classification
- **Source**: architecture review
- **Category**: technology
- **Impact**: high
- **Confidence**: confirmed
- **Status**: pending
- **Actionable**: Yes
- **Tags**: testing, integration-tests, type-safety, ci-pipeline, technical-debt


