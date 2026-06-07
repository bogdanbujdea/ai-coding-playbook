---
name: summarize-for-review
description: Create a review handoff for completed or partially completed implementation work, summarizing the request, approach, changed files, validation, risks, and review focus areas.
argument-hint: "What should the reviewer focus on?"
---

# Handoff Review

Create a review-focused handoff for a fresh agent.

Use this after implementing a feature, fix, refactor, migration, or other change that should be reviewed by another agent.

The goal is to brief the reviewer, not perform the review.

## Behavior

- If arguments were provided, treat them as the review focus.
- Summarize what was requested and how it was implemented.
- Do not paste large code blocks.
- Do not continue implementing, refactoring, debugging, or reviewing.
- Do not duplicate content already captured in PRDs, plans, ADRs, issues, commits, diffs, PRs, or previous handoffs. Reference those artifacts by path or URL.

## Output File

Save the handoff under `.tmp/` in the workspace root. Create `.tmp/` if needed.

Use a unique title-based filename:

```text
.tmp/YYYY-MM-DD-HHMM-brief-review-title.md