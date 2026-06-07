---
name: to-prd
description: Turn the current conversation context into a PRD saved as a local markdown file. Use when user wants to create a PRD from the current context.
---

This skill takes the current conversation context and codebase understanding and produces a PRD whose implementation is broken down into **vertical slices**. Do NOT interview the user — just synthesize what you already know.

The PRD is written as a local, disposable markdown file. Publishing the slices as tracked work items is delegated to the `to-issues` skill at the end.

## Process

1. Explore the repo to understand the current state of the codebase, if you haven't already. If `docs/domain.md` is present, use its vocabulary throughout the PRD; if `docs/architecture.md` is present, respect the decisions it records. Proceed silently if either is absent.

2. Sketch out the major modules you will need to build or modify to complete the implementation. Actively look for opportunities to extract deep modules that can be tested in isolation.

A deep module (as opposed to a shallow module) is one which encapsulates a lot of functionality in a simple, testable interface which rarely changes.

Check with the user that these modules match their expectations. Check with the user which modules they want tests written for.

3. Break the implementation down into **vertical slices** following the guidance below. Confirm the slice list with the user before publishing.

4. Write the PRD using the template below to a local markdown file at:

   ```
   .features/<feature-name>-<YYYY-MM-DD>/PRD.md
   ```

   - `<feature-name>` is a kebab-cased slug derived from the PRD topic; `<YYYY-MM-DD>` is today's date. Example: `.features/implement-authentication-with-google-2026-05-13/PRD.md`.
   - The vertical slices live inside the PRD as a checklist.
   - `.features/` holds disposable planning artifacts — the user deletes a feature folder when its work is done. Ensure `.features/` is listed in `.gitignore`; add it if it is missing (create `.gitignore` if the repo has none).

5. Offer to publish the slices as tracked work items by **invoking the `to-issues` skill**, passing this PRD's vertical-slice list as the plan. If the user declines, stop here — the PRD file is the deliverable.

## Vertical Slice Guidance

The guiding principle is the **tracer bullet** (from *The Pragmatic Programmer*): build the tiniest possible end-to-end slice of the feature first — one that cuts through every layer and produces real, observable output — so you get feedback as early as possible. You then *expand out* from that working skeleton, deepening behavior slice by slice. The first slice exists to validate the approach and surface architectural problems before significant time is invested, not to be feature-complete.

A vertical slice is a piece of work that cuts through every layer it touches (UI → API → domain → data, or whatever layers apply) and delivers an observable, demonstrable change in behavior. It is the opposite of a horizontal slice (e.g. "set up the database", "scaffold the service", "wire the UI") which on its own delivers nothing a person can see.

Rules for the slices you propose:

- **Slice 1 is the tracer bullet.** Make it the smallest thing that runs end-to-end through all layers and produces visible output, even if it hard-codes values, handles only the happy path, or covers one trivial case. Its job is to prove the path works and invite feedback. Every later slice expands behavior outward from it.
- **Each slice must be manually testable by a dev or QA.** If you cannot write a short "to verify, do X and observe Y" instruction, it is not a slice — fold it into the first real slice that needs it.
- **No purely horizontal/infrastructure-only slices.** Setup work (migrations, scaffolding, new packages, feature flags, config) rides along with the first vertical slice that requires it.
- **Balance size for reviewability vs. throughput.** Use the judgement of a senior developer who knows the codebase: small enough that a reviewer can hold the diff in their head in one sitting, large enough that you are not creating churn from artificially tiny slices. There is no fixed LOC or file-count rule — calibrate to the requirement at hand.
- **Order slices so each one builds on the previous** and the system stays shippable (behind a flag if needed) after every slice.

<prd-template>

## Problem Statement

The problem that the user is facing, from the user's perspective.

## Solution

The solution to the problem, from the user's perspective.

## User Stories

A focused, numbered list of user stories — one per **distinct user-facing outcome**, in the format:

1. As an <actor>, I want a <feature>, so that <benefit>

<user-story-example>
1. As a mobile bank customer, I want to see balance on my accounts, so that I can make better informed decisions about my spending
</user-story-example>

Keep the list **proportional to the feature's real scope** — it should track the vertical slices below, not pad them out. A small feature has a few stories, not dozens. Do **not** enumerate every field, screen state, or near-duplicate variation as its own story (e.g. "change the date", "change the amount", "change the description" collapse into one "edit an expense's fields"). If two stories would map to the same observable behavior, merge them. Cover every meaningful outcome once; stop there.

## Implementation Decisions

A list of implementation decisions that were made. This can include:

- The modules that will be built/modified
- The interfaces of those modules that will be modified
- Technical clarifications from the developer
- Architectural decisions
- Schema changes
- API contracts
- Specific interactions

Do NOT include specific file paths or code snippets. They may end up being outdated very quickly.

## Vertical Slices

An ordered checklist of vertical slices that together implement this PRD. Each slice must be independently demonstrable and manually verifiable. Setup/infrastructure work is folded into the first slice that needs it — no horizontal-only slices. Slice sizing is a senior-developer judgement call: small enough to review comfortably in one sitting, large enough to avoid death-by-a-thousand-PRs.

For each slice:

- [ ] **<Slice title>**
  - **Delivers:** what the user (or operator/dev, if internal) can newly do or observe after this slice ships.
  - **Manual verification:** concrete steps to exercise the slice and the expected observable outcome.
  - **Depends on:** prior slices, if any.
  - **Notes:** flags, migrations, or other context that ride along with this slice.

## Testing Decisions

A list of testing decisions that were made. Include:

- A description of what makes a good test (only test external behavior, not implementation details)
- Which modules will be tested
- Prior art for the tests (i.e. similar types of tests in the codebase)
- Which slices warrant automated coverage in addition to the manual verification scenario

## Out of Scope

A description of the things that are out of scope for this PRD.

## Further Notes

Any further notes about the feature.

</prd-template>