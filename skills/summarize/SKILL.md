---
name: summarize
description: Create a concise handoff document that summarizes the current conversation for a fresh agent, including goal, context, decisions, references, and next steps.
argument-hint: "What will the next session be used for?"
---

# Handoff

Create a compact handoff document for a fresh agent.

Use this for general conversation summaries, planning sessions, brainstorming, research, or context transfer.

For debugging sessions with many attempted fixes, use `/summarize-debugging`.
For implementation review handoffs, use `/summarize-for-review`.

## Behavior

- Summarize only information needed by the next agent.
- If arguments were provided, treat them as the next session focus.
- Do not continue implementation, debugging, review, or investigation.
- Do not duplicate content already captured in PRDs, plans, ADRs, issues, commits, diffs, or previous handoffs. Reference those artifacts by path or URL.

## Output File

Save the handoff under `.tmp/` in the workspace root. Create `.tmp/` if needed.

Use a unique title-based filename:

```text
.tmp/YYYY-MM-DD-HHMM-brief-conversation-title.md