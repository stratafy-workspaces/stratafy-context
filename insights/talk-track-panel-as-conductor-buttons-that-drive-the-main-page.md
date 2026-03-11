---
id: 1eaf6a8f-2c45-452a-b086-655eb00056a9
type: insight
source: stratafy_chat
category: product
impactLevel: high
confidenceLevel: likely
status: pending
actionable: true
---

# Talk track panel as conductor — buttons that drive the main page

## Summary
The talk track panel shouldn't just show narrative text — it should be a remote control for the main page. Buttons in the panel drive exactly what appears on the main page: which node is active, which tab is open, which metric is visible. The presenter looks only at the panel. The audience looks only at the main page. The panel is the conductor; the page is the stage.

## Description
Current model: talk track panel shows text + step navigation. User has to manage both panel and tree simultaneously — reading the panel, then clicking around the tree to show the right thing.

Better model: the panel is a remote control. Every action in the panel has a precise, intentional effect on the main page.

**Button types in the panel:**

1. **Next / Prev** — advances the step, auto-expands the correct node, opens the contextually correct tab for the audience mode, scrolls to the node. No manual interaction with the tree required.

2. **Reveal buttons** — inline within the talk track text, contextually placed:
   - "Show metrics →" → opens Metrics tab on current node, panel slightly narrows so both are readable
   - "See the initiatives →" → opens Initiatives tab, scrolls initiative list into view
   - "Show assumptions →" → opens Assumptions tab, highlights validated ones
   - "Drill in →" → expands into a child strategy, maintaining flow context

3. **Zoom controls:**
   - "Zoom in" → navigates into a child node as if it's the new root, breadcrumb trail shows path back
   - "Back to flow" → returns to the flow's parent node and resumes the step sequence

4. **Highlight controls:**
   - "Highlight this metric" → pulses or rings a specific metric card on the main page to draw audience eye
   - "Focus here" → temporarily dims everything except the current node (full focus mode)

**The interaction model this creates:**
- Presenter looks only at the panel — reads talk track, clicks buttons, never touches the tree directly
- Audience looks only at the main page — sees a clean, controlled, intentional reveal of information
- The presentation feels choreographed rather than improvised
- No risk of accidentally clicking the wrong node or losing your place

**Why this matters for the demo:**
This is what separates a "feature demo" from a "product experience." When the presenter controls the story from a single panel and the page responds precisely, the audience experiences the product as something that works for you, not something you work around.

**Implementation notes:**
- Reveal buttons are inline markdown-style in the talk track text: `[Show metrics →](action:open-tab:metrics)`
- Button actions are a typed enum: `open-tab`, `scroll-to-node`, `highlight-metric`, `zoom-in`, `focus-mode`
- Panel state and main page state are kept in sync via a shared `presentationState` context
- Keyboard shortcuts: space/right arrow = next, left arrow = prev, number keys = jump to tab

## Classification
- **Source**: stratafy chat
- **Category**: product
- **Impact**: high
- **Confidence**: likely
- **Status**: pending
- **Actionable**: Yes
- **Tags**: presentation-mode, panel-conductor, remote-control, ux, demo-experience


