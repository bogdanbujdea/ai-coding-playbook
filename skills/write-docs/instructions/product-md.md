# `docs/product.md` instruction

## Purpose

Document what the product or project does so an AI coding agent can make context-aware changes.

This doc should describe product behavior and user-facing purpose, not implementation details.

## Output file

```text
docs/product.md
```

## When to create or update

Create this file by default for project documentation tasks.

## Sources to inspect

- `README.md`
- existing docs
- route names
- UI copy
- page titles
- API names
- package or app names
- tests that describe behavior
- seed data or sample data
- user-provided context

## Required content

Cover:

1. What the product/project is.
2. Who uses it.
3. The core problem it solves.
4. Key workflows or user journeys.
5. Whether this repo is standalone or part of a larger system.
6. Important external systems or integrations, only if relevant to product behavior.
7. Product boundaries: what this project does not do, if known.

## Recommended structure

```markdown
# Product overview

## Summary

<One or two paragraphs describing the product.>

## Users

- <User/persona> — <what they do in the product>

## Core workflows

- <Workflow> — <short description>
- <Workflow> — <short description>

## Project context

- Standalone or part of larger system: <answer or Not documented yet>
- Related projects/services: <answer or Not documented yet>

## External product dependencies

- <System> — <why it matters to product behavior>

## Out of scope

- <Known product boundary>
```

## What to avoid

Do not include:

- setup commands
- detailed infrastructure
- CI/CD behavior
- generic business claims
- marketing language
- invented personas
- unverified roadmap items
- implementation file paths unless necessary

## Accuracy rules

- Product claims must come from code, docs, tests, UI text, or user context.
- If the project purpose is unclear, say `Not documented yet` instead of guessing.
- Do not infer customers, personas, or business model from package names alone.
- Keep integrations brief here; detailed operational information belongs in other docs.

## Self-check

Before finishing, confirm:

- The summary is understandable without reading the code.
- The workflows are grounded in observed behavior.
- No implementation details dominate the doc.
- Unknown product context is marked clearly.
