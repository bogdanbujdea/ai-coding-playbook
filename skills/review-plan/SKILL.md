---
name: review-plan
description: Review an implementation plan against the current codebase before execution. Use when the user asks to review, audit, stress-test, verify, or reality-check a plan for correctness, scope, assumptions, file paths, consistency with existing codebase patterns, risks, edge cases, or validation gaps.
---

# Review Plan

Review the provided implementation plan impartially before execution.

Your job is not to approve the plan.
Your job is not to find issues for the sake of finding issues.
Your job is to determine whether the plan is accurate, appropriately scoped, consistent with the codebase when available, and safe to execute.

Be pragmatic, evidence-based, and honest.

## Core Behavior

When this skill is used:

1. Read the full plan before commenting.
2. Identify the stated goal of the plan.
3. Inspect only relevant codebase files before making claims about files, symbols, APIs, tests, commands, architecture, or conventions.
4. Compare the plan against the actual codebase when the codebase is available.
5. Report confirmed problems, uncertainties, design concerns, and things that appear sound.
6. Do not implement the plan.
7. Do not edit files.
8. Do not rewrite the plan unless the user explicitly asks for a revised version.
9. Produce a concise copy/paste summary that the user can paste back into the original planning conversation.

Default mode is review-only.

## If Codebase Is Unavailable

If the codebase is unavailable, do not make codebase-specific claims.

Review only:

- goal clarity
- internal consistency
- scope fit
- sequencing
- risk
- validation

Label the result as a plan-only review.

Do not claim that files, symbols, commands, tests, routes, components, database fields, or codebase patterns exist or do not exist.

## Goal Clarity

Before reviewing details, check whether the plan has a clear goal.

The goal is clear only if the plan explains:

- what user-visible or externally verifiable behavior should change
- what counts as done
- the intended scope of the change

If the goal is unclear enough that correctness cannot be judged, stop and ask for clarification.

If some parts can still be reviewed safely, provide only those observations and clearly label the result as a limited review.

Do not review a plan against an inferred goal unless the user explicitly asks you to make assumptions.

## Review Depth

Scale the review to the size and risk of the plan.

For small plans, keep the review short and focus only on:

- goal clarity
- codebase accuracy, if codebase is available
- consistency with existing patterns, if codebase is available
- scope fit
- validation

For medium or large plans, use the full review structure.

For risky plans, pay extra attention to sequencing, reversibility, data safety, authorization, migrations, production behavior, and validation.

## Relevance Rule

Only inspect files and behavior directly related to the plan.

Do not perform a broad architecture review.
Do not search for unrelated improvements.
Do not review code style unless the plan depends on it.
Do not recommend refactors unless they are necessary for the stated goal.
Do not expand the plan beyond what is needed to achieve the goal safely.

## Review Focus

Check the plan for the following.

### 1. Goal Clarity

Determine whether the goal is specific enough to review.

Flag vague goals such as:

- "improve the flow"
- "clean this up"
- "make it better"
- "fix the feature"

Recommend a clearer goal when possible.

### 2. Codebase Accuracy

When the codebase is available, verify that the plan references real codebase elements.

Check:

- file names
- file paths
- components
- functions
- classes
- routes
- schemas
- commands
- tests
- configuration files
- package scripts
- existing patterns

Do not assume a file, symbol, command, or pattern exists. Inspect the codebase.

### 3. Codebase Consistency

When the codebase is available, check whether the plan follows the existing patterns used in the relevant part of the codebase.

Look for consistency in:

- API style
- controller structure
- routing patterns
- request and response models
- service boundaries
- repository usage
- database access patterns
- error handling
- validation style
- naming conventions
- test structure
- frontend state management
- component organization
- formatting utilities
- dependency usage

Flag inconsistencies when the plan proposes a different pattern without explaining why.

Examples:

- The codebase uses controllers, but the plan proposes minimal endpoints.
- The codebase uses repository classes, but the plan directly accesses the database context.
- The codebase uses Redux selectors, but the plan bypasses them.
- The codebase uses existing API response models, but the plan introduces an unrelated DTO style.
- The codebase has a date formatting utility, but the plan creates a second formatter.

Do not require consistency for its own sake. A different pattern is acceptable when the plan gives a clear reason and the change is appropriate for the goal.

### 4. Wrong Assumptions

Identify assumptions in the plan and classify them as:

- Confirmed
- Contradicted
- Not verified

A contradicted assumption is an issue only when it affects the plan’s execution or correctness.

### 5. Scope Fit

Check whether the plan is larger than needed for the stated goal.

Flag unnecessary:

- refactors
- abstractions
- rewrites
- architecture changes
- documentation updates
- broad test rewrites
- unrelated cleanup
- changes outside the feature area

Prefer vertical slices over horizontal technical phases.

A good plan should produce small, testable behavior increments.

### 6. Missing Behavior or Edge Cases

Look for important missing cases directly related to the goal.

Consider:

- empty states
- loading states
- error states
- permission or authorization behavior
- invalid input
- data consistency
- backward compatibility
- existing users or existing data
- failure recovery
- accessibility when relevant
- mobile or responsive behavior when relevant

Do not list generic edge cases that are unrelated to the goal.

### 7. Sequencing

Check whether the steps are ordered safely.

Flag steps when:

- a later step depends on something not created yet
- validation happens too late
- risky changes are made before simple verification
- the plan mixes unrelated changes in one step
- the plan cannot be paused after a useful vertical slice

### 8. Validation

Check whether the plan includes concrete validation.

Good validation includes known commands or explicit manual checks.

Examples:

- run the known test command
- run the known build command
- verify a specific UI behavior
- test a specific API response
- confirm a specific database state
- check a specific error path

Flag vague validation such as:

- "make sure it works"
- "test everything"
- "verify the feature"
- "check for regressions"

### 9. Risk and Reversibility

Identify risky steps.

Examples:

- data migrations
- destructive operations
- authentication or authorization changes
- payment or billing changes
- broad dependency upgrades
- generated file changes
- changes to shared utilities
- changes to public APIs
- changes that affect production behavior

Recommend isolating risky changes when possible.

## Impartiality Rules

Do not invent issues.

Do not nitpick harmless stylistic choices.

Do not claim something is wrong unless you can explain why it matters.

Do not treat uncertainty as a confirmed problem.

Do not over-recommend tests, docs, or refactors.

Do not praise the plan vaguely.

When something appears correct, say so briefly.

Use "No issue found" only for sections included in the chosen output format.

Do not enumerate every review category for small plans.

## Evidence Rules

For every concrete issue, include evidence.

Use this structure:

- Plan says:
- Codebase shows:
- Why it matters:
- Recommended change:

If evidence cannot be found, classify it as a question or uncertainty.

Do not say a file is missing until you have searched for likely alternatives.

Do not say a command exists unless you inspected the project scripts or relevant documentation.

Do not say a pattern is inconsistent unless you inspected nearby existing code.

## Design Recommendation Rule

Separate confirmed execution problems from design recommendations.

A confirmed execution problem is contradicted by the codebase or makes the plan impossible to execute as written.

A design recommendation is an alternative that may be cleaner, safer, more conventional, or more consistent, but is not strictly required.

Do not label a design recommendation as a blocker unless the current plan is unsafe, impossible, or clearly incorrect.

Use "Design concern" when the plan may work but uses a questionable or inconsistent approach.

## Schema Change Rule

When recommending database columns, persisted fields, migrations, or schema changes, explain why each new field is necessary.

For each suggested field, state:

- what value it stores
- who writes it
- who reads it
- why the value cannot be derived from existing state

Do not add persistence fields only because they seem convenient.

Do not recommend schema changes without checking the existing persistence pattern, unless this is a plan-only review. In a plan-only review, mark schema recommendations as questions or design concerns.

## Severity

Classify each finding as one of:

- Blocker: the plan is unsafe, unclear, or cannot be executed as written.
- Major: likely to cause implementation failure, wrong behavior, or unnecessary complexity.
- Minor: worth fixing, but does not block execution.
- Design concern: the plan may work, but conflicts with existing patterns or uses a questionable approach.
- Question: cannot be resolved from the codebase or plan alone.

Use the lowest severity that accurately describes the issue.

## Output Format

For small plans, use this shorter format:

```md
# Plan Review

## Verdict

Ready to execute / Ready with minor changes / Needs revision / Unsafe or unclear

Briefly explain the verdict.

## Findings

- List confirmed issues, questions, or "No confirmed issues found."

## Suggested Plan Patch

- Replace:
- Add:
- Remove:
- Reorder:
- Clarify:

Only include relevant patch items.

## Validation

List concrete validation steps.

## Copy/Paste Summary for Original Planning Conversation

Provide a concise markdown block that the user can paste into the original planning conversation.

Include only the important corrections and questions.

Do not include the entire review.
```

For medium, large, or risky plans, use this full format:

```md
# Plan Review

## Verdict

Ready to execute / Ready with minor changes / Needs revision / Unsafe or unclear

Briefly explain the verdict.

## Goal Being Reviewed

State the plan’s goal in one sentence.

## Confirmed Issues

Group by severity.

For each issue, use:

- Plan says:
- Codebase shows:
- Why it matters:
- Recommended change:

If there are no confirmed issues, write:

No confirmed issues found.

## Design Concerns

List non-blocking design concerns separately.

Use this section for recommendations that may improve consistency, safety, maintainability, or sequencing but are not confirmed blockers.

If there are no design concerns, write:

No important design concerns found.

## Questions / Unverified Assumptions

List only questions or unverified assumptions that affect execution, correctness, safety, or scope.

If none, write:

No important unresolved questions found.

## What Looks Sound

Briefly list parts of the plan that appear accurate, safe, or well-scoped.

Keep this section short.

## Codebase Consistency

State whether the plan follows existing patterns.

List only meaningful inconsistencies that affect maintainability, implementation success, or integration with the existing code.

If the codebase is unavailable, omit this section.

If no consistency problems are found, write:

No important consistency issues found.

## Scope Notes

State whether the plan is appropriately sized for the goal.

Mention unnecessary complexity or missing vertical slices if relevant.

## Missing Edge Cases

List only edge cases relevant to the stated goal.

If none, write:

No important missing edge cases found.

## Validation

List concrete validation steps.

Prefer known commands from the codebase when available.

## Suggested Plan Patch

Provide concise changes the user can paste back into the planning conversation.

Use one or more of:

- Replace:
- Add:
- Remove:
- Reorder:
- Clarify:

Do not rewrite the whole plan unless explicitly asked.

## Copy/Paste Summary for Original Planning Conversation

Provide only the important corrections and questions.
```

## Copy/Paste Summary Rules

The copy/paste summary is required.

Keep it short.

Write it as if the user will paste it into the original planning conversation.

Use direct instructions.

Prefer this format:

```md
## Review Findings to Apply

Please update the plan with these findings:

1. ...

2. ...

3. ...

Questions to resolve before implementation:

- ...
```

Include only:

- confirmed blockers or major issues
- important design concerns
- important consistency issues
- unresolved questions that affect the plan
- concrete suggested edits

Do not include:

- the full review
- long evidence tables
- minor observations unless they change the plan
- praise
- repeated context

The summary should usually be less than 25% of the full review.

## Optional Parallel Review

For medium, large, or risky plans, consider splitting the review into independent read-only review lanes.

Use parallel agents or subagents only if the current coding environment supports them and the user has allowed parallel work.

Do not require parallel agents. If parallel execution is unavailable, perform the same review sequentially.

Suggested review lanes:

1. File and symbol verification
   - Verify file paths, modules, components, functions, routes, schemas, commands, tests, and configuration references.
   - Report only confirmed mismatches or unverified references.

2. Assumption verification
   - Extract explicit and implicit assumptions from the plan.
   - Classify each as Confirmed, Contradicted, or Not verified.

3. Consistency review
   - Check whether the plan follows existing patterns in the relevant codebase area.
   - Report meaningful inconsistencies only when they affect maintainability, implementation success, or integration.

4. Scope and sequencing review
   - Check whether the plan is too broad, too complex, or ordered unsafely.
   - Identify unnecessary refactors, horizontal slices, risky sequencing, or missing vertical slices.

5. Edge case and validation review
   - Check for relevant missing behavior, failure states, permissions, data consistency issues, and concrete validation steps.

Each review lane must be read-only.

After all lanes finish, synthesize the results into one final review.

Deduplicate findings.
Resolve conflicts between reviewers.
Do not include a finding in the final review unless it is relevant to the stated goal.
Clearly mark unresolved disagreements as questions.

## If the User Asks You to Update the Plan

Only update or rewrite the plan when the user explicitly asks.

When updating the plan:

1. Preserve the original goal.
2. Apply only review findings that are confirmed or accepted by the user.
3. Keep the plan smaller rather than larger.
4. Prefer vertical slices.
5. Preserve useful existing plan structure.
6. Do not add unrelated improvements.
7. Keep the updated plan consistent with existing codebase patterns.

## Final Response Rule

End with one of these:

- "This plan is ready to execute."
- "This plan is ready after the minor changes above."
- "This plan should be revised before execution."
- "This plan is unclear or unsafe to execute as written."