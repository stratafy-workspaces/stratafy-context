---
id: 79985d6b-1f85-4902-a9ae-732626b41b2e
type: insight
source: stratafy_chat
category: operational
impactLevel: high
confidenceLevel: confirmed
status: processed
actionable: true
lastUpdated: 2026-02-06T08:22:24.266766+00:00
---

# Test-first bug fixing: reproduce before you fix

## Summary
Don't start fixing a bug by trying to fix it. Start by writing a failing test that reproduces it. Then fix. The test proves understanding and prevents false fixes.

## Description
When an AI agent is asked to fix a bug, it should NOT start by attempting to fix it. Instead: (1) Write a test that reproduces the bug and fails, (2) Have subagents attempt fixes, (3) Prove the fix with the test passing. This ensures the bug is understood before fixing, prevents false fixes, creates regression protection, and enables parallel attempts with an objective arbiter. Source: @dyokomizo on X.

## Classification
- **Source**: stratafy chat
- **Category**: operational
- **Impact**: high
- **Confidence**: confirmed
- **Status**: processed
- **Actionable**: Yes
- **Tags**: bug-fixing, testing, ai-agents, workflow, best-practice, claude-code


