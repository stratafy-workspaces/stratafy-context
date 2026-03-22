---
id: ee35296e-9752-43da-9971-e164dde98d5b
type: insight
source: architecture_review
category: product
impactLevel: critical
confidenceLevel: likely
status: pending
actionable: true
---

# MCP coaching prompts are the product differentiator — depth here outweighs additional CRUD tools

## Summary
The MCP server grew from ~10 to 169+ tools, but the real product value concentrates in the 4-5 coaching prompts (Coach Me, Advise Me, Let's Go, review_strategy_tree). Making these contextually intelligent — pulling health scores, provenance trends, alignment gaps, signal patterns — is higher leverage than adding more CRUD tools. A Coach Me prompt that says "your Product Strategy health dropped 15% and 3 assumption changes weren't reflected in objectives" is worth more than 50 additional tools.

## Description
## Maps To
- **Strategic Delivery** → Context Intelligence v2 (query-intent routing)
- **Strategic AI Infrastructure** → MCP Server Optimisation
- **Strategic Delivery** → Stratafy Leadership Team plugins

## Recommendation
Invest in making coaching prompts pull from: health scores (already built), provenance trends (already built), alignment scan results (already built), signal patterns (already built). The infrastructure exists — the gap is wiring these into the prompt context so the coaching feels genuinely intelligent rather than generic.

## Evidence
The Week 3 decision to add Coach Me/Advise Me/Let's Go prompts was the inflection point where MCP became a product, not just an API. Usage tracking was wired to prompts in the same week — suggesting you already sensed this was the high-value surface.

## Classification
- **Source**: architecture review
- **Category**: product
- **Impact**: critical
- **Confidence**: likely
- **Status**: pending
- **Actionable**: Yes
- **Tags**: mcp, coaching-prompts, strategic-delivery, product-differentiation


