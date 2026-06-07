---
name: write-docs
description: Project documentation toolkit. Invoke ONLY when the user types `/write-docs` or makes an unambiguous request to write, update, audit, or refactor project documentation files (`AGENTS.md`, `CLAUDE.md`, `docs/`, per-folder `README.md`). Do not invoke for ambiguous asks like 'document this', 'add a README', 'write release notes', or any code-comment or single-file documentation request.
---

# Write Project Docs

## Purpose

Create or update project-specific documentation that helps AI coding agents and human maintainers understand the repository accurately.

The goal is not to create a large documentation site. The goal is to create a small, reliable documentation set that captures stable project knowledge and points agents to the right places.

Use progressive disclosure:

- Keep `AGENTS.md` short.
- Put detailed project knowledge in focused files under `docs/`.
- Use one target document per documentation type.
- Do not mix generic engineering preferences into project docs.

## Trigger

See this skill's `description` for the authoritative invocation rules.

## Scope levels

Project documentation lives at three scopes. Each scope has a different file and different rules.

| Scope | File | Purpose |
|---|---|---|
| Root | `AGENTS.md` (+ `CLAUDE.md` referencing it) | Repo-wide orientation. Links to project docs. ≤ 50 lines. |
| Package or feature folder | `<folder>/README.md` | Conventions specific to that folder only. ≤ 40 lines. |
| Cross-repo container | None | When multiple sibling repos live under one opened folder, do not write a global root file. Treat each child repo independently. |

Per-folder rules use `README.md` because it is portable across Cursor, Claude Code, Copilot, and other tools, and because folders that already have a `README.md` can absorb the rules without adding a new file type.

Do not create nested `AGENTS.md` files inside packages or feature folders by default.

## Review mode

Review mode audits existing project documentation and proposes changes. It is a separate operating mode from writing new docs.

### When to enter Review mode

Enter Review mode when the user asks to:

- audit project docs
- review project docs
- refactor `AGENTS.md` or `CLAUDE.md`
- check if docs are bloated, stale, or contradictory
- clean up `docs/`

Also enter Review mode when, during normal inspection, you discover that the repo already has substantial project docs (for example: `AGENTS.md` over 50 lines, multiple files under `docs/`, an existing `CLAUDE.md` with project content, `.cursorrules`, or `.github/copilot-instructions.md`). In that case, ask the user before writing anything:

```markdown
This repo already has project docs:
- `<file>` (<N> lines)
- `<file>` (<N> lines)

How should I proceed?
1. Review and refactor under the standard structure.
2. Keep the current structure; only fix specific issues I find.
3. Leave existing docs alone; only add what is missing.
```

Do not refactor existing docs without explicit approval.

### Review mode flow

Use `instructions/review.md` as the writing specification for the audit. It defines the discovery sources, the audit checklist, and the report format.

The flow is:

1. **Discover** existing docs across all known locations.
2. **Audit** them against the checklist in `instructions/review.md`.
3. **Report** findings to the user grouped by severity.
4. **Wait** for the user's choice (refactor / fix-specific / leave as is).
5. **Act** only on what the user approved.

Do not modify any file during discovery or audit. Reports are read-only.

## Documentation set

Default project docs:

```text
AGENTS.md
docs/
  product.md
  domain.md
  local-development.md
  infrastructure.md
  ci-cd.md
```

Optional docs:

```text
docs/
  architecture.md
  testing.md
  release.md
  observability.md
  security.md
  <area>.md  (language, framework, or workflow conventions — see below)
```

### Conventions docs

When the *Inspect before writing* step finds language-, framework-, or workflow-specific rules in existing `AGENTS.md`, `CLAUDE.md`, linter config, or formatter config, propose one conventions doc per area instead of inlining rules in root `AGENTS.md`.

Common names: `docs/typescript.md`, `docs/python.md`, `docs/csharp.md`, `docs/api.md`, `docs/git.md`, `docs/sql.md`, `docs/styling.md`.

Use `instructions/conventions-md.md` when writing these files.

Do not create a conventions doc for an area with no project-specific rules.

### Per-package and per-feature `README.md`

When the *Inspect before writing* step detects a monorepo, workspaces, or a vertical-slice / feature-folder layout, also propose a per-folder `README.md` for each package or feature with conventions distinct from the root.

Use `instructions/feature-readme-md.md` when writing these files.

Do not propose a per-folder `README.md` for folders that have nothing folder-specific to say. A folder that follows root conventions exactly does not need one.

## Mandatory behavior

### 1. Inspect before writing

Before proposing or editing docs, inspect the repository.

Look for:

- existing `README.md`, `AGENTS.md`, `CLAUDE.md`, and `docs/`
- package manifests and workspace files
- build, test, and run commands
- CI/CD configuration
- deployment and infrastructure configuration
- Docker or compose files
- application entry points
- route definitions or service boundaries
- test projects and test frameworks
- logging, metrics, tracing, and error tracking configuration
- authentication, authorization, tenancy, and permission code
- domain terms in code, docs, tests, schemas, routes, and UI copy

Also detect repository shape:

- **Cross-repo container**: multiple `.git/` directories under the opened root, or sibling folders that each contain their own root manifest. If detected, do not write a global root `AGENTS.md`. Document each child repo independently or ask the user which child repo to document.
- **Monorepo / workspaces**: `pnpm-workspace.yaml`, `package.json` with a `workspaces` field, `turbo.json`, `nx.json`, `lerna.json`, a Cargo workspace, a .NET solution with multiple projects, or a `packages/` or `apps/` directory with multiple manifests. If detected, list packages in the root `AGENTS.md` and propose a per-package `README.md` for each package with non-trivial conventions.
- **Vertical-slice / feature folders**: a `Features/`, `features/`, `modules/`, or `slices/` directory whose subfolders repeat the same internal structure (for example, each contains endpoint, validator, handler, and persistence files). If detected, propose a per-feature `README.md` for each feature instead of a single top-level architecture doc.

Prefer source files, config files, scripts, and existing docs over inference.

### 2. Propose the structure before creating files

After inspection, present the proposed documentation structure and ask the user which files should not be created or updated.

Use this format:

```markdown
I propose creating or updating this documentation structure:

Default project docs:
- `AGENTS.md` — short project orientation for AI agents; links to the docs below.
- `docs/product.md` — what the product does, who uses it, key workflows, and project context.
- `docs/domain.md` — domain glossary and stable project concepts.
- `docs/local-development.md` — tech stack, setup, commands, and local runtime dependencies.
- `docs/infrastructure.md` — hosting, deployed environments, services, and runtime dependencies.
- `docs/ci-cd.md` — pipelines, validation jobs, deployment jobs, secrets, and dependencies.

Optional docs recommended for this repo:
- `docs/<optional>.md` — <reason this repo appears to need it>.

I do not plan to create by default:
- `docs/environment.md`
- `docs/data-model.md`
- `docs/migrations.md`
- standalone integration docs

Are there any files in this structure that should not be created or updated right now?
```

If the user already specified the exact files to create, do not ask again. Use their list.

When creating or updating `AGENTS.md`, also ask the user which issue tracker this repo uses — `azure-devops`, `github`, or `local-markdown` — defaulting to the auto-detected option (an Azure DevOps MCP server is connected → `azure-devops`; a `github.com` git remote → `github`; otherwise `local-markdown`). Record the answer as a single line in `AGENTS.md` (see `instructions/agents-md.md`). The `to-prd` and `to-issues` skills read this line as their default backend. Skip the question if such a line already exists and the user has not asked to change it.

### 3. Create a shared fact base before parallel work

Before assigning parallel doc writers or writing multiple docs, create a shared fact base in the task context. Use this structure internally; write it to a temporary planning note only if the user approves. All doc writers must use the same shared fact base.

```markdown
# Documentation facts

## Project identity
- Name:
- Product type:
- Main purpose:
- Part of a larger system:

## Tech stack
- Languages:
- Runtime:
- Frameworks:
- Package manager:
- Database:
- Queue/background jobs:
- Hosting:
- CI/CD:

## Verified commands
- Install:
- Run locally:
- Build:
- Test:
- Typecheck:
- Lint:

## Important domain terms
- Term:
- Term:

## Environments and services
- Local:
- Staging:
- Production:
- External services:

## Evidence reviewed
- `path/to/file`
- `path/to/file`
```

Mark unknown values explicitly; do not invent. List inspected files under `Evidence reviewed` so reviewers can trace facts.

### 4. Use focused instructions for each doc

Use the matching file in `instructions/` when writing each target doc:

```text
instructions/agents-md.md              -> AGENTS.md
instructions/product-md.md             -> docs/product.md
instructions/domain-md.md              -> docs/domain.md
instructions/local-development-md.md   -> docs/local-development.md
instructions/infrastructure-md.md      -> docs/infrastructure.md
instructions/ci-cd-md.md               -> docs/ci-cd.md
instructions/architecture-md.md        -> docs/architecture.md
instructions/testing-md.md             -> docs/testing.md
instructions/release-md.md             -> docs/release.md
instructions/observability-md.md       -> docs/observability.md
instructions/security-md.md            -> docs/security.md
instructions/conventions-md.md         -> docs/<area>.md  (typescript, python, api, git, ...)
instructions/feature-readme-md.md      -> <package or feature folder>/README.md
instructions/review.md                 -> Review mode audit (see below)
```

When parallelizing, assign each worker exactly one target file and its matching instruction file.

### 5. One target file per parallel worker

For parallel doc writing, each worker must receive the target file path, the matching instruction file, the shared fact base, the source files to inspect, and a rule to modify only the target file. Use this worker prompt pattern:

```text
Write or update only `<target-file>`.

Use `<instruction-file>` as the writing specification.
Use the shared fact base as the common source of truth.
Inspect only the source files relevant to this doc unless more evidence is required.

Do not modify any other file.
Do not invent missing facts.
If a fact is not discoverable, write `Not documented yet` or omit the section if omission is safer.
Keep the doc short and project-specific.
```

Workers must not modify peer docs, even to fix contradictions; surface contradictions to the reconciliation pass instead.

### 6. Reconcile after parallel work

After all docs are drafted, perform a single reconciliation pass.

Check that:

- project name is consistent everywhere
- package manager is consistent everywhere
- commands are consistent everywhere
- domain terms match `docs/domain.md`
- `AGENTS.md` links only to docs that exist
- `CLAUDE.md` references `AGENTS.md` if `CLAUDE.md` exists
- CI/CD and release docs do not contradict each other
- infrastructure and observability docs do not contradict each other
- security and architecture docs do not contradict each other
- no doc contains invented facts
- unknowns are marked clearly
- no doc duplicates long sections from another doc
- generic coding or testing preferences were not added

## File rules

- Prefer updating existing docs over creating new files.
- Do not overwrite existing docs wholesale when a focused edit is enough.
- Create the `docs/` directory only if approved or clearly required by the requested files.
- Do not delete documentation files unless the user explicitly approves deletion.
- Do not move documentation files unless the user explicitly asks.
- Do not modify production code.
- Do not modify tests unless the user explicitly asks.
- Do not modify CI/CD, infrastructure, or application config while documenting.
- Never include real secrets, private keys, tokens, passwords, or credentials.

## Accuracy rules

- Every factual claim must be grounded in inspected files, user-provided context, or clearly marked as unknown.
- Do not infer hosting, deployment, or CI/CD behavior from naming alone.
- Do not claim a command works unless it exists in scripts, config, docs, or was run successfully.
- Do not document file paths that are not useful or likely to remain stable.
- Prefer stable concepts, workflows, commands, and system boundaries over detailed file trees.
- Do not say a service is used in production unless production usage is verified.
- Do not say tests exist unless test files, test projects, or test commands are found.
- Do not say a project has observability unless logging, metrics, tracing, dashboards, alerts, or error tracking are found.
- Do not say a project has role-based access control unless roles or permissions are found.
- If evidence conflicts, stop and ask the user which source is authoritative.

## Style rules

- Be concise.
- Use headings and short bullets.
- Use tables only when they improve clarity.
- Avoid generic advice.
- Avoid motivational language.
- Avoid “best practices” unless they are concrete project facts.
- Use `Not documented yet` for important missing information that the user should fill in.
- Prefer links between docs instead of duplicating content.
- Keep examples short and executable when possible.

## Validation

After writing docs:

1. Check that every created link points to an existing file.
2. Check that commands match package manifests, build files, scripts, or existing docs.
3. Check that optional docs are referenced only if they were created.
4. Check that `AGENTS.md` is short and links to detailed docs.
5. If `CLAUDE.md` exists, ensure it references `AGENTS.md` instead of duplicating the same project instructions.
6. Report any commands that were not verified.
7. Report any unknowns left as `Not documented yet`.

Run documentation checks if the repository provides them.

Examples:

```bash
pnpm docs:check
npm run docs:check
make docs
```

Only run commands that are present or clearly documented.

## Final response format

After completing the work, respond with:

```markdown
Created or updated:
- `<file>` — <short description>
- `<file>` — <short description>

Validation:
- <checks performed>
- <commands run, if any>
- <links checked>

Not verified:
- <facts or commands that could not be verified>

Follow-ups:
- <specific missing information the user should provide, if any>
```

Keep the response short. List every file created or modified. Be explicit about facts that could not be verified. Use `Follow-ups` to ask for specific missing inputs, not generic next steps.
