# Conventions doc instruction

## Purpose

Document language-, framework-, or area-specific conventions that an AI coding agent must follow when writing code in that scope.

This file exists so root `AGENTS.md` does not carry rules that only apply to a subset of tasks.

## Output file

```text
docs/<area>.md
```

Common areas: `docs/typescript.md`, `docs/python.md`, `docs/csharp.md`, `docs/api.md`, `docs/git.md`, `docs/sql.md`, `docs/styling.md`.

Use one file per area. Do not bundle unrelated areas in a single file.

## When to create or update

Create or update this file when the repository has rules specific to one language, framework, or workflow area that should not live in root `AGENTS.md`.

Do not create this file for areas with no project-specific rules. A repo that uses standard idioms for a language does not need a conventions doc for it.

## Sources to inspect

- existing `AGENTS.md` and `CLAUDE.md` (rules to be moved out)
- existing `docs/` files
- linter and formatter configuration (`.eslintrc`, `tsconfig.json`, `pyproject.toml`, `.editorconfig`, `.prettierrc`, `.editorconfig`, ruleset files)
- code style observable in source files
- existing per-folder `README.md` files for rules that should be promoted to repo-wide

## Required content

Cover only what is project-specific in this area:

1. One-sentence scope statement (what area this doc covers).
2. Concrete rules grounded in linter config, formatter config, or observed patterns.
3. Patterns to use, patterns to avoid, with one short example each when needed.
4. Links to related conventions docs, only if they exist.

## Recommended structure

```markdown
# <Area> conventions

<One-sentence scope statement.>

## Rules

- <Concrete rule grounded in config or observed pattern>
- <Concrete rule grounded in config or observed pattern>

## Patterns

- Use: <pattern>
- Avoid: <pattern>

## See also

- <Link to a related conventions doc, if any>
```

## Size budget

Keep the file focused. Target under 80 lines. If the file grows past 80 lines, split it by sub-area (for example, split `docs/typescript.md` into `docs/typescript.md` + `docs/react.md`).

## What to avoid

- Generic engineering advice ("write clean code", "use clear names").
- Rules already enforced by the linter or formatter without further nuance.
- Patterns the language or framework already requires by default.
- Rules that belong in a different scope (architecture, testing, security).
- Long rationale; state the rule, then a one-line reason only if non-obvious.
- File paths that are likely to drift.

## Accuracy rules

- Every rule must be grounded in linter config, formatter config, observed code, or explicit user input.
- Do not invent style rules to fill gaps; if no convention exists in the repo, omit the topic.
- If a rule contradicts the linter config, ask the user which is authoritative.

## Self-check

Before finishing, confirm:

- The file covers exactly one area.
- Every rule is concrete and grounded.
- No rule could be moved back to root `AGENTS.md` and apply universally.
- The file does not duplicate root `AGENTS.md` or other conventions docs.
- Every link resolves.
