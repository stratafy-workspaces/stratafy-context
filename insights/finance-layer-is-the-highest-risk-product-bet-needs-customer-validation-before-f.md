---
id: aaa6dc01-8f98-4dc1-9d6f-8400a70691cf
type: insight
source: architecture_review
category: product
impactLevel: high
confidenceLevel: likely
status: pending
actionable: true
---

# Finance layer is the highest-risk product bet — needs customer validation before further investment

## Summary
The Finance layer (COA proposals, KaTeX formula rendering, AI-driven model generation, strategy-to-account mappings) is the most complex domain-specific layer built. It's also where strategy becomes concrete — budgets and burn rates are where real decisions happen. But if customers don't engage with conversational model-building, it's significant surface area to maintain. Recommend getting it in front of 2-3 customers specifically to validate the AI financial model interaction pattern.

## Description
## Maps To
- **Core Product Capabilities** → Finance Layer initiative (in_progress, high priority)
- **Product-Market Fit** strategy (validation question)

## Risk
Finance is the layer most likely to either become a killer feature or dead weight. It pulled the platform into "where real decisions get made" territory architecturally, but the conversational model-building UX hasn't been validated with users yet.

## Recommendation
Run targeted validation with 2-3 customers. Specifically test: (1) Does conversational financial model building land? (2) Do strategy-to-account mappings help with budget allocation decisions? (3) Is KaTeX formula rendering actually useful or is a simpler format sufficient?

## Evidence
14 commits in a single week, including AI chat panel, KaTeX rendering, tool schema simplification for Zod v4 issues — this was a deep investment.

## Classification
- **Source**: architecture review
- **Category**: product
- **Impact**: high
- **Confidence**: likely
- **Status**: pending
- **Actionable**: Yes
- **Tags**: finance-layer, customer-validation, product-risk, core-capabilities


