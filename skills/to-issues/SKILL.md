---
name: to-issues
description: Break a plan, spec, or PRD into independently-testable issues and publish them to the repo's issue tracker (Azure DevOps, GitHub, or local markdown). Use when the user wants to convert a plan into issues, create implementation tickets, or break down work into issues.
---

# To Issues

Break a plan into independently-grabbable issues using vertical slices.

## Process

### 1. Gather context

If you were invoked by the `to-prd` skill, use the PRD's vertical-slice list as the input plan — do not re-derive it from scratch. Otherwise, work from whatever is already in the conversation context. If the user passes an issue reference (issue number, URL, or path) as an argument, fetch it from the resolved issue tracker (see step 5) and read its full body and comments.

### 2. Explore the codebase (optional)

If you have not already explored the codebase, do so to understand the current state of the code. If `docs/domain.md` is present, use its vocabulary for issue titles and descriptions; if `docs/architecture.md` is present, respect the decisions it records. Proceed silently if either is absent.

### 3. Draft issues

Break the plan into issues using the **tracer bullet** principle (from *The Pragmatic Programmer*): build a tiny, end-to-end slice of the feature first, seek feedback, then expand out from there. Produce the **minimum number** of independently-testable issues — do not decompose further unless the user explicitly requests it.

<vertical-slice-rules>
- The **first issue is the tracer bullet**: the smallest slice that runs end-to-end through every layer and produces visible output, even if it hard-codes values or covers only the happy path. Order it first so feedback comes early; every later issue expands behavior outward from it.
- Each issue must be a **complete, functional unit of behavior** that a human can manually trigger and verify in isolation — no other pending issues need to be merged first to observe the correct result
- Do NOT create issues that implement only a single layer (e.g., only a DB schema change, only an API endpoint, only a UI component) — each issue must include all layers required for the behavior to work end-to-end
</vertical-slice-rules>

### 4. Quiz the user

Present the proposed breakdown as a numbered list in dependency order (issues that must be completed first appear earlier in the list). For each issue, show:

- **Title**: short descriptive name
- **Description**: one sentence describing the end-to-end behavior it delivers

Ask the user:

- Do you want any of these split into smaller issues?
- Is the order correct?

Iterate until the user approves the breakdown.

### 5. Resolve the issue tracker

Once the user has approved the issue list, decide which backend to publish to. The supported backends are `azure-devops`, `github`, and `local-markdown`.

1. Look for an `Issue tracker:` line in `AGENTS.md` (then `CLAUDE.md`). If present, use its value as the **proposed default**.
2. Otherwise auto-detect a default:
   - An Azure DevOps MCP server is available in this session → `azure-devops`
   - `git remote -v` contains `github.com` and the `gh` CLI is available → `github`
   - otherwise → `local-markdown`
3. **Always ask** the user to confirm or choose among `azure-devops` / `github` / `local-markdown`, pre-selecting the detected default.

Proceed to the matching step below.

### 6a. Publish as local markdown files

Write one `.md` file per issue under `.features/<feature-name>-<YYYY-MM-DD>/issues/`, numbered in dependency order from `01`: `NN-<kebab-title>.md`. Reuse the same `<feature-name>-<date>` folder as the PRD if one exists (e.g. when invoked by `to-prd`); otherwise create a new one. Use the issue body template below. Ensure `.features/` is listed in `.gitignore`; add it if missing (create `.gitignore` if the repo has none).

### 6b. Publish to Azure DevOps

Use the Azure DevOps MCP server. **Classify each issue** — do not ask the user which type to use; decide based on the issue's nature:
- **ADO User Story** — the issue describes user-visible behavior or a feature the user can interact with
- **ADO Task** — the issue describes purely technical implementation work with no direct user-facing surface

Show the user your classification for every issue before creating anything. Correct any classification the user disagrees with.

Then ask the user for the required parent work item IDs:
- For any issues classified as **ADO User Story**: ask for the parent **Feature ID**
- For any issues classified as **ADO Task**: ask for the parent **User Story ID**

If all issues share the same parent, a single ID is sufficient. If there are mixed types or multiple parents, collect each ID explicitly.

Create the ADO work items in dependency order (blockers first) so real ADO work item IDs can be referenced in the "Blocked by" field. Do NOT close or modify the parent Feature or User Story.

### 6c. Publish to GitHub

Use the `gh` CLI. `gh` infers the repo from `git remote -v` when run inside a clone.

Create one issue per item with `gh issue create --title "..." --body "..."` (use a heredoc for the multi-line body, built from the template below). Create the issues in dependency order (blockers first) so real issue numbers can be referenced in the "Blocked by" field of later issues.

---

<issue-template>
## Description

A concise description of the end-to-end behavior this issue delivers. Describe what the user or system can do after this issue is complete — not a layer-by-layer breakdown of implementation steps.

## Acceptance criteria

- [ ] Criterion 1 (manually verifiable: describe exactly what a human should do and observe)
- [ ] Criterion 2
- [ ] Criterion 3

## Prerequisites for testing

Steps a human must complete before testing can begin — things the AI agent cannot do automatically. Examples: applying configuration changes, setting feature flags, running a CI/CD pipeline, provisioning infrastructure, seeding data, or obtaining credentials.

- Prerequisite 1
- Prerequisite 2

## How to test

A walkthrough of what to verify once the issue is deployed. Cover what changed and what to watch for — do not just restate the acceptance criteria.

- **UI changes**: describe any new or modified screens, components, or interactions to check
- **Infrastructure / config changes**: describe any environment-level changes to verify (e.g., new resource visible in portal, pipeline green, config value applied)
- **Existing user flows**: describe any previously working flows that touch this area and should still work correctly

## Blocked by

ADO work item ID or filename of the blocking issue, or "None — can start immediately".

</issue-template>
