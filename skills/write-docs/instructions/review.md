# Review mode instruction

## Purpose

Audit existing project documentation and report findings so the user can decide whether to refactor, fix specific issues, or leave the docs alone.

Review mode never modifies files during the audit. Modifications happen only after the user approves them.

## Output

A single audit report sent to the user as a chat message. No files are written during the audit phase.

## Sources to inspect

- `AGENTS.md` (root and any nested copies)
- `CLAUDE.md`
- `README.md` at the root and inside packages or feature folders
- `docs/**/*.md`
- `CONTRIBUTING.md`
- `.cursorrules`, `.cursor/rules/**`
- `.github/copilot-instructions.md`
- any other markdown file the user identifies as project documentation

## Audit checklist

For each discovered file, check:

### Size

- Root `AGENTS.md` over 50 lines.
- Per-folder `README.md` (in a package or feature folder) over 40 lines.
- Any single doc file in `docs/` that is unusually long for its scope.

### Bloat

- Generic coding rules (for example: "use clear variable names", "write clean code").
- Generic testing rules not specific to this repo's tooling.
- Generic security advice not tied to a concrete repo hazard.
- Motivational language or restated industry "best practices".

### Vague

- Instructions too generic to act on (for example: "be careful with errors", "keep things simple", "think before coding").
- Instructions that restate something the model already knows by default.
- Instructions without a concrete trigger, target, or outcome.

### Contradictions

- The same fact stated differently across files (commands, package manager, project name, domain terms, environment names).
- Instructions in one file that conflict with instructions in another.

### Stale paths

- File paths referenced in docs that no longer exist or have moved.
- Architecture descriptions that mention obsolete folders or files.

### Dead links

- Markdown links to files or anchors that do not resolve.
- External links that are clearly broken (optional; only if obvious).

### Duplication

- Sections that appear nearly verbatim in more than one file.
- `CLAUDE.md` duplicating `AGENTS.md` content instead of referencing it.
- `.cursorrules` re-stating things already in `AGENTS.md`.

### Missing essentials

- Root `AGENTS.md` lacks a one-line project description.
- Root `AGENTS.md` lacks a non-standard package manager note when one applies.
- Root `AGENTS.md` lacks links to existing project docs.
- Repo has feature folders or packages but no `Packages / features` section in `AGENTS.md`.

### Tool drift

- Instructions written for one tool (Cursor, Copilot, Claude Code) duplicated across other tool-specific files instead of being centralized in `AGENTS.md`.

## Report format

Send the report as a single chat message using this structure:

```markdown
# Documentation audit

## Files discovered

- `<path>` (<N> lines)
- `<path>` (<N> lines)

## Findings

### Block (must resolve before refactor)
- `<file>`: <contradiction, stale path, or dead link>

### Delete (recommended)
- `<file>` line <N>: <vague, redundant, or obvious instruction — quote it>

### Trim (recommended)
- `<file>`: <bloat, duplication, or size overflow>

### Add (recommended)
- `<file>`: <missing essential>

### Refactor option (structural)
- <One-line proposal, e.g. "Move TypeScript conventions out of `AGENTS.md` into `docs/typescript.md`.">

## Contradictions to resolve

For each contradiction under Block, list both versions and ask the user which to keep:

- `<file-a>` says: "<quote>"
- `<file-b>` says: "<quote>"
- Which version should I keep?

## How would you like to proceed?

1. Review and refactor under the standard structure.
2. Keep the current structure; only fix the items I pick.
3. Leave existing docs alone; only add what is missing.
```

If a category has no findings, omit the entire subsection. Always include the `Contradictions to resolve` section when at least one contradiction exists, and block on the user's answer before any rewrite.

## Accuracy rules

- Every finding must point to a specific file and a specific issue. No vague comments.
- Do not report a contradiction unless both versions are quoted or paraphrased accurately.
- Do not report a stale path without confirming the path does not exist.
- Do not report a dead link without confirming the link target is missing.
- Do not invent missing essentials; check the actual file content.

## What to avoid

- Do not modify any file during Review mode.
- Do not propose deletions of user-authored docs without explicit user approval.
- Do not rewrite sections in the report; the report is a list of findings, not a draft.
- Do not include a finding the user cannot act on.

## Self-check

Before sending the report, confirm:

- Every file inspected is listed under "Files discovered".
- Every finding is grounded in inspected content.
- Every Delete and Vague finding quotes the offending instruction.
- Every contradiction lists both versions and asks the user which to keep.
- The three-way user choice is present at the end of the report.
- The report does not contain rewritten content.
