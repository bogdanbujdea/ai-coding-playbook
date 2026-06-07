---
name: summarize-debugging
description: Create a debugging reset handoff for a fresh agent, preserving the issue, reproduction, impacted files, commands run, attempted fixes, failures, findings, and what not to retry.
argument-hint: "What should the next debugging session focus on?"
---

# Handoff Debug

Create a debugging reset handoff for a fresh agent.

Use this when a long debugging session included failed attempts, diagnostic work, errors, failing tests, or multiple changed/inspected files.

The goal is to prevent the next agent from repeating failed work.

## Behavior

- If arguments were provided, treat them as the next debugging focus.
- Preserve evidence, attempted fixes, failed assumptions, impacted files, and next steps.
- Do not continue debugging or try another fix.
- Do not duplicate content already captured in issues, logs, diffs, commits, PRs, or previous handoffs. Reference those artifacts by path or URL.

## Output File

Save the handoff under `.tmp/` in the workspace root. Create `.tmp/` if needed.

Use a unique title-based filename:

```text
.tmp/YYYY-MM-DD-HHMM-brief-debug-title.md