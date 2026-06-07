# `docs/domain.md` instruction

## Purpose

Document the stable domain vocabulary and conceptual model of the project.

This is mandatory because AI agents often hallucinate when project terms are ambiguous.

This is not a database schema document.

## Output file

```text
docs/domain.md
```

## When to create or update

Create this file by default for project documentation tasks.

## Sources to inspect

- existing docs
- UI labels and page names
- API route names
- database model names
- entity names in code
- test names
- fixtures and seed data
- authorization logic
- user-provided product context

## Required content

Cover:

1. Glossary of important terms.
2. Relationships between terms.
3. Terms that are easy to confuse.
4. Project-specific meanings that differ from common usage.
5. Naming constraints or domain invariants, if verified.

## Recommended structure

```markdown
# Domain glossary

## Core concepts

### <Term>

<Definition in this project.>

Related terms:
- <Related term>

Important notes:
- <Constraint or distinction>

## Relationships

- `<Term A>` contains/owns/relates to `<Term B>` in this way: <description>.

## Common confusions

- `<Term A>` is not the same as `<Term B>`. <Explain the difference.>
```

## What to include

Good entries:

```markdown
### Organization

A customer-owned container for users, projects, and billing configuration.
```

```markdown
### Run

A single execution of an automation workflow.
```

## What to avoid

Do not include:

- a full database schema
- migration history
- every model/class name
- implementation file paths
- generic dictionary definitions
- terms that appear only once and do not affect understanding
- unverified business assumptions

## Accuracy rules

- Define only terms found in code, docs, tests, UI text, schema names, or user context.
- Do not invent hierarchy.
- If two terms appear to be synonyms, mark the uncertainty instead of collapsing them.
- Prefer stable conceptual relationships over field-level detail.
- If tenancy or ownership is important and verified, include it.

## Self-check

Before finishing, confirm:

- Important project-specific terms are defined.
- Ambiguous terms are disambiguated.
- The doc does not duplicate database schema details.
- Definitions match usage across the repo.
