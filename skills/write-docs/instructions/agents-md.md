# `AGENTS.md` instruction

## Purpose

Create a short root-level orientation file for AI coding agents.

`AGENTS.md` should help an agent begin work in the repository without loading all project knowledge into the root context. It should point to focused docs instead of duplicating them.

## Output file

```text
AGENTS.md
```

## When to create or update

Create or update this file when the user wants project documentation for AI agents.

If a root `AGENTS.md` already exists, preserve useful instructions and reduce bloat where possible.

If `CLAUDE.md` exists, update it only enough to reference `AGENTS.md`, unless the user asks for more.

## Sources to inspect

- existing `AGENTS.md`
- existing `CLAUDE.md`
- `README.md`
- package manifests
- workspace files
- docs directory
- common command scripts
- project configuration files

## Size budget

The entire file must stay at or under 50 lines, including blank lines and headings. If the content does not fit, move material into linked docs. Do not shrink by removing blank lines or merging sections; shrink by relocating content.

## Required content

Include only information relevant to nearly every agent task:

1. One-sentence project description.
2. Package manager or primary build tool, only if non-standard for the language ecosystem.
3. Repo-specific commands that an agent could not correctly guess.
4. Links to project docs.
5. Navigation hints for workspace packages or feature folders, if the repo has them.
6. A single `Issue tracker:` line, if the user specifies one (see below).

Omit anything that does not match this list.

### Issue tracker line

If the user has chosen an issue tracker for this repo, record it as one line:

```markdown
Issue tracker: azure-devops
```

Allowed values: `azure-devops`, `github`, `local-markdown`. The `to-prd` and `to-issues` skills read this line as their default publishing backend. Keep it to a single line (a short `## Issue tracker` heading is optional but counts against the 50-line budget — a bare line near the top is fine). Omit it entirely if the user has no preference.

## Recommended structure

```markdown
# Agent instructions

<One-sentence project description.>

## Commands

- <Only commands that are non-standard, package-manager-specific, or repo-specific scripts.>

## Project docs

- Product overview: `docs/product.md`
- Domain glossary: `docs/domain.md`
- Local development: `docs/local-development.md`
- Infrastructure: `docs/infrastructure.md`
- CI/CD: `docs/ci-cd.md`

## Packages / features

- `<folder>` — <one-line purpose, see `<folder>/README.md`>
```

### Commands rule

- Omit commands an agent would correctly guess (`npm install`, `npm test`, `dotnet build`, `cargo build`).
- Include only commands tied to a non-default package manager (`pnpm`, `uv`, `bun`), repo-specific scripts, or commands with non-obvious arguments.
- Do not include any command that has not been verified against scripts, manifests, or existing docs.

### Safety section rule

Omit a `Repository-specific safety` section unless the repo has a concrete, repo-wide hazard worth one short bullet (for example: a shared dev database, a destructive migration command, or a deploy script that hits production by default). Generic safety advice does not belong here.

### Packages and features rule

Include a `Packages / features` section only when the repo is a monorepo, uses workspaces, or follows a feature-folder layout. List each folder once with a one-line purpose and a path agents can read on demand. Per-folder rules belong in that folder's `README.md`, not in `AGENTS.md`.

Only link to docs that exist or are being created in the same documentation task.

## What to avoid

Do not include:

- detailed architecture
- long file trees
- generic coding rules
- generic testing rules
- generic security advice
- full CI/CD descriptions
- full infrastructure descriptions
- full domain glossary
- tool-specific instructions that belong in `CLAUDE.md`, Cursor rules, Copilot instructions, or another tool config

## `CLAUDE.md` handling

If `CLAUDE.md` exists, make it reference `AGENTS.md`.

Minimal acceptable content:

```markdown
# Claude instructions

Use the shared project instructions in `AGENTS.md`.
```

If `CLAUDE.md` contains Claude-specific instructions that are not duplicated in `AGENTS.md`, preserve them.

Do not duplicate the full contents of `AGENTS.md` inside `CLAUDE.md`.

## Accuracy rules

- Do not claim a command exists unless verified.
- Do not link to a doc that does not exist or is not being created.
- Do not document exact file paths unless they are stable and useful.
- Mark missing important information as `Not documented yet` only when it belongs in `AGENTS.md`; otherwise link to the relevant doc.

## Self-check

Before finishing, confirm:

- `AGENTS.md` is at or under 50 lines.
- It links to detailed docs instead of duplicating them.
- All links resolve.
- Commands are non-standard or repo-specific only; obvious commands are omitted.
- No `Repository-specific safety` section unless a concrete repo-wide hazard exists.
- A `Packages / features` section exists if and only if the repo is a monorepo, uses workspaces, or has feature folders.
- `CLAUDE.md`, if present, references `AGENTS.md`.
