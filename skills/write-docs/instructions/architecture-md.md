# `docs/architecture.md` instruction

## Purpose

Document the project's system architecture at a conceptual level.

This doc should help an AI coding agent understand boundaries, flows, and constraints without needing a full code walkthrough.

## Output file

```text
docs/architecture.md
```

## When to create or update

Create this file only when approved or when the repo is complex enough to need it.

Recommend it when the repo has:

- multiple apps
- multiple packages
- backend and frontend boundaries
- background workers
- queues or events
- multiple deployable services
- complex auth or tenancy
- non-obvious request/data flow

## Sources to inspect

- existing architecture docs
- `README.md`
- package/app structure
- route definitions
- service entry points
- queue/worker definitions
- API clients
- infrastructure config
- CI/CD deployment jobs
- tests that describe integration boundaries
- user-provided context

## Required content

Cover:

1. High-level system shape.
2. Main components or deployable units.
3. Request flow.
4. Data flow.
5. Background or async processing, if present.
6. Important boundaries.
7. Architecture constraints or tradeoffs, if verified.
8. Links to related docs.

## Recommended structure

```markdown
# Architecture

## Summary

<Short description of the system shape.>

## Components

- <Component> — <responsibility>

## Request flow

1. <Step>
2. <Step>
3. <Step>

## Data flow

- <Source> → <Processor> → <Storage/output>

## Background processing

- <Worker/job/queue> — <purpose>

## Boundaries and constraints

- <Verified constraint>

## Related docs

- Domain glossary: `domain.md`
- Infrastructure: `infrastructure.md`
- CI/CD: `ci-cd.md`
```

## What to avoid

Do not include:

- long file trees
- every class/module
- speculative diagrams
- database schema details
- local setup commands
- deployment pipeline details
- generic architecture advice
- unverified tradeoffs

## Accuracy rules

- Do not invent components.
- Do not infer async processing unless queue, worker, scheduler, or job code is visible.
- Do not claim service boundaries unless deployable units or package boundaries support it.
- Prefer conceptual boundaries over volatile file paths.
- If the architecture is simple, say so and keep the doc short.

## Self-check

Before finishing, confirm:

- The doc explains how the system fits together.
- The component list is not just a file tree.
- Flows are evidence-backed.
- Related docs are linked only if they exist.
