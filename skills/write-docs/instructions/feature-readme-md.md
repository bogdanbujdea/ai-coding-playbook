# Per-folder `README.md` instruction

## Purpose

Document conventions specific to one package or feature folder so an AI coding agent (or human) reads only the rules that apply when working inside that folder.

This file complements root `AGENTS.md`. It does not replace it.

## Output file

```text
<package or feature folder>/README.md
```

## When to create or update

Create or update this file when the repository has a monorepo, workspaces, or a vertical-slice / feature-folder layout, and the folder has conventions distinct from the root.

Do not create this file for folders that follow root conventions exactly.

## Sources to inspect

- existing `README.md` in the folder
- code in the folder (entry points, route handlers, validators, persistence, tests)
- package manifest in the folder, if present
- existing root `AGENTS.md` and `docs/` so the file does not duplicate them

## Required content

Cover only what is specific to this folder:

1. One-sentence scope description.
2. Folder-specific conventions (naming, layering, validation, persistence, error handling) that differ from the rest of the repo.
3. Folder-specific commands, only if any exist.
4. Links to deeper docs in this folder, only if they exist.

## Recommended structure

```markdown
# <Folder name>

<One-sentence scope description.>

## Conventions

- <Folder-specific rule>
- <Folder-specific rule>

## Commands

- <Only commands that run from this folder and are non-obvious.>

## See also

- <Path to a deeper doc inside this folder, if any>
```

## Size budget

The entire file must stay at or under 40 lines, including blank lines and headings.

## What to avoid

Do not include:

- repo-wide conventions that already live in root `AGENTS.md` or root `docs/`
- the project's overall purpose
- generic engineering rules
- generic testing rules
- the same content repeated across multiple feature folders (move it to root if it is shared)
- detailed file paths that drift quickly

## Accuracy rules

- Every claim must be grounded in code, manifests, or existing docs in this folder.
- Do not document a convention unless it is observable in this folder's code.
- If a folder has no rules distinct from the root, delete the file or do not create it; do not pad it with restated root content.

## Self-check

Before finishing, confirm:

- The file is at or under 40 lines.
- It contains only folder-specific content.
- It does not duplicate root `AGENTS.md` or root `docs/`.
- Every link resolves.
