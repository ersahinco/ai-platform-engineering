# Contributor Tooling

This page is the maintenance map for the root-level AI and editor tooling files in this repository.

The goal is simple: contributors should be able to tell which files are product code, which files are project policy, and which files are duplicated compatibility shims for specific tools.

## Why This Matters

This repository supports multiple AI-assisted workflows. That makes it easy for contributors to use different tools, but it also creates drift risk when files look similar and no one can tell which copy is authoritative.

Use this page as the source of truth before editing:

- `AGENTS.md`
- `CLAUDE.md`
- `.claude/`
- `.cursor/`
- `.specify/`
- `skills/`
- `.beads/`

## Maintenance Categories

### Hand-Maintained Project Policy and Context

These files are part of the repo's contributor workflow and should be edited directly when the project policy or contributor guidance changes:

- `AGENTS.md`
- `CLAUDE.md`
- `.specify/ARCHITECTURE.md`
- `.specify/CHANGELOG.md`
- `.specify/README.md`
- `.specify/SKILLS.md`
- `.specify/SPECS.md`
- `.specify/TESTING.md`
- `.specify/memory/constitution.md`
- `skills/README.md`
- `skills/*/SKILL.md`

### Synced Editor Command Packs

These files provide the same `speckit.*` commands to different editors:

- `.cursor/commands/speckit.*.md`
- `.claude/commands/speckit.*.md`

Current repo state:

- the documented canonical source directory, `.specify/templates/commands/`, is not present in the repository
- the command packs are therefore checked in directly as synced duplicates
- if you change one shared `speckit.*` command, change the matching file in both directories in the same commit

### Editor-Specific Files

These files are not shared command-pack duplicates and should be treated as tool-specific:

- `.claude/commands/run-caipe-integration-tests.md`
- `.cursor/rules/specify-rules.mdc`
- `.cursorrules`

Edit these only when the tool-specific behavior itself needs to change.

## Safe Maintenance Rules

- Do not treat contributor-tooling files as part of the product runtime surface.
- Do not move or delete tool-specific directories just because they look noisy.
- Keep shared `speckit.*` command changes mirrored across `.cursor/commands/` and `.claude/commands/`.
- Keep tool-specific files separate from shared command-pack updates.
- Prefer documenting current state honestly over claiming a generation pipeline that does not exist in the repo.

## `make generate-agent-commands`

The `Makefile` still includes `make generate-agent-commands`, but it is currently a guarded target.

That target now fails with an explanatory message if `.specify/templates/commands/` is missing. This is intentional. A clear failure is safer than silently generating editor command packs from a nonexistent or partial source.

## Preferred Future Direction

The maintainable target is still:

1. restore a real canonical command source under `.specify/templates/commands/`
2. generate `.cursor/commands/` and `.claude/commands/` from that source
3. keep tool-specific extras such as `.claude/commands/run-caipe-integration-tests.md` outside the shared command-generation path

Until that source is restored, treat the checked-in command packs as synced compatibility copies and update them carefully.
