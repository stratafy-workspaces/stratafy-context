---
id: f55ef2c3-6ec6-44fc-a3bf-9c5113b9bb27
type: insight
source: stratafy_chat
category: product
impactLevel: critical
confidenceLevel: likely
status: pending
actionable: true
---

# Conversational agent with live page control — the AI-native interaction model

## Summary
A chat window where the agent doesn't just respond in text — it navigates the strategy page, opens modals, highlights data, and writes to the workspace in real time as you talk. The page is the canvas. The conversation is the interface. This is the AI-native interaction model that separates Stratafy from every legacy strategy tool.

## Description
## The concept

A persistent chat window — available on any page in Stratafy — where a context-aware agent can both converse with you AND control the main strategy page simultaneously.

This is distinct from Story Mode (scripted, presenter-led, audience-facing). The chat agent is live, exploratory, and responsive to wherever the conversation goes.

## What makes it different from a normal chat window

Most AI chat in SaaS tools is isolated — you ask a question, you get a text answer, you go back to clicking around the UI. The agent described here has a live connection to the page. When it wants to show you something, it shows you — it doesn't just describe it.

You ask: "What's the biggest risk to the partner channel strategy?"
The agent navigates the tree to the Partner Ecosystem Channel node, opens the Risks tab, surfaces the risk modal for the highest-scored risk — and says "Let me show you."

The conversation and the page are one experience.

## The three things the agent can do

### 1. Navigate
- Move the tree to any strategy node
- Open any tab (Strategy, Objectives, Metrics, Assumptions, Initiatives, Risks, Insights)
- Zoom in/out of the tree
- Scroll to any entity
- All using the same action vocabulary as Story Mode's conductor (STR-196)

### 2. Surface
- Open any modal (Metrics, Assumptions, Risk, Initiative Snapshot, Decisions)
- Highlight and pulse specific metric cards
- Trigger focus mode on a node
- All using the same modal system (STR-198)

### 3. Write
- Log a decision: "Note that as a decision" → creates a decision record linked to the current strategy
- Capture a risk: "That's a risk we should track" → creates a risk, asks for severity
- Update an assumption: "Mark that assumption as validated" → updates status
- Create an insight: "That's an important observation" → logs to insights
- Update initiative status: "Move that to in progress" → updates the initiative

The third capability is what makes this genuinely AI-native — the chat is not just a query interface, it's a way of building the workspace through conversation.

## The relationship to Story Mode

Story Mode and the chat agent share the same underlying page-control API. Story Mode uses it in scripted sequence (pre-generated talk track). The chat agent uses it responsively (live, based on conversation). Building the conductor system (STR-196) correctly means both surfaces use the same primitives — navigate, surface, modal. No duplication.

## What it enables in practice

**Client sessions:** Walk a client through their workspace conversationally. They ask questions, the agent shows them the answers on the page. The session feels like a guided exploration, not a demo.

**Internal strategy work:** Think out loud with the agent. "I'm not sure the partner channel assumptions hold." Agent pulls up the assumptions, you review them together, you update them in the same conversation.

**Investor prep:** "Show me everything that supports the moat argument." Agent navigates to relevant nodes, surfaces metrics, pulls assumptions — building the narrative for you in real time.

**Onboarding:** New workspace member asks "where does X fit?" Agent navigates them to the right place, explains context, answers follow-up questions — all without leaving the page.

## Why this is the AI-native interaction model

Legacy SaaS: you work in the tool, AI is a helper in a sidebar.
AI-native: the conversation IS the interface, the page responds to it, and thinking + acting happen in the same flow.

The chat window isn't a feature. It's the primary way of operating Stratafy for users who think in language rather than clicks — which is most strategic thinkers.

## Classification
- **Source**: stratafy chat
- **Category**: product
- **Impact**: critical
- **Confidence**: likely
- **Status**: pending
- **Actionable**: Yes
- **Tags**: ai-native, chat-agent, page-control, interaction-model, north-star


