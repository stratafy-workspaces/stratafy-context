---
id: 988af48a-1753-40b5-b404-9f12dff58be7
type: insight
source: stratafy_chat
category: technology
impactLevel: high
confidenceLevel: likely
status: pending
actionable: true
---

# Stratafy's 169-tool MCP surface area requires context-aware tool gating

## Summary
With 169+ MCP tools, Stratafy is a prime example of the "monolithic context anti-pattern" described by Aroussi. The Chat SDK and multi-platform access layers need classification gates and selective tool injection to avoid consuming 20-30% of context windows with tool schemas that aren't needed for the current request.

## Description
Ran Aroussi's article crystallizes a problem Stratafy will face at scale: loading all 169+ tool definitions into every conversation consumes thousands of tokens before the user's actual task even begins. The proposed architecture — a classification gate that determines whether tools are needed, combined with selective injection of only relevant tool schemas — is directly applicable to Stratafy's Chat SDK strategy and the multi-platform access layer. This should inform the Product Architecture strategy, specifically how the Chat SDK packages strategic context alongside tool definitions without blowing out the context budget. The "treat context as a budget, not a log" principle applies to both tool schemas and the strategic context Stratafy injects (workspace snapshots, strategy trees, etc.).

## Classification
- **Source**: stratafy chat
- **Category**: technology
- **Impact**: high
- **Confidence**: likely
- **Status**: pending
- **Actionable**: Yes
- **Tags**: mcp, context-window, chat-sdk, product-architecture, agent-infrastructure


