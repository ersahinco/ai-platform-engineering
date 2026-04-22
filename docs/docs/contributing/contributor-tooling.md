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

This page covers contributor tooling only. For runtime-oriented root files such as `prompt_config.yaml`, `task_config.yaml`, `policy.lp`, `persona.yaml`, and `slim-config.yaml`, see the ownership notes below before treating them as clutter.

## Maintenance Categories

### Canonical Project Policy and Shared Context

These files are the canonical source for repo-wide contributor policy and shared AI workflow context. Edit these when the project guidance itself changes:

- `AGENTS.md`
- `.specify/ARCHITECTURE.md`
- `.specify/CHANGELOG.md`
- `.specify/README.md`
- `.specify/SKILLS.md`
- `.specify/SPECS.md`
- `.specify/TESTING.md`
- `.specify/memory/constitution.md`
- `skills/README.md`
- `skills/*/SKILL.md`

For shared repo policy, prefer `AGENTS.md` as the canonical top-level entrypoint. The supporting docs in `docs/` and `skills/*/SKILL.md` should stay consistent with it.

### Tool-Specific Entry Points and Wrappers

These files exist to meet specific editor or agent entrypoint conventions. They may repeat project policy, but they should not invent a different version of it:

- `CLAUDE.md`
- `.cursorrules`
- `.cursor/rules/specify-rules.mdc`

If a tool-specific wrapper diverges from `AGENTS.md` on shared repo policy, treat that as documentation drift to fix.

Keep wrappers thin. They should point contributors back to `AGENTS.md` for shared repo policy and contain only the minimum tool-specific behavior that cannot live elsewhere.

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

### Root Runtime Compatibility Files

These files live at the repository root, but they are not contributor-tooling noise:

- `prompt_config.yaml`: root symlink to `charts/ai-platform-engineering/data/prompt_config.yaml`
- `task_config.yaml`: root symlink to `charts/ai-platform-engineering/data/task_config.yaml`
- `policy.lp`: root symlink to `charts/ai-platform-engineering/data/policy.lp`
- `persona.yaml`: input for `scripts/generate-docker-compose.py`
- `slim-config.yaml`: local transport configuration used by Docker Compose and workshop flows

Treat these as local runtime and compatibility entrypoints. Do not remove or move them unless the compose, workshop, chart, and UI/API references are updated together.

## Safe Maintenance Rules

- Do not treat contributor-tooling files as part of the product runtime surface.
- Do not treat runtime compatibility files at the repo root as disposable clutter just because they sit next to contributor-tooling files.
- Do not move or delete tool-specific directories just because they look noisy.
- Keep shared `speckit.*` command changes mirrored across `.cursor/commands/` and `.claude/commands/`.
- Keep tool-specific files separate from shared command-pack updates.
- Keep tool-specific wrappers minimal and avoid restating general repo policy in multiple places.
- Prefer documenting current state honestly over claiming a generation pipeline that does not exist in the repo.

## `make generate-agent-commands`

The `Makefile` still includes `make generate-agent-commands`, but it is currently a guarded target.

That target now fails with an explanatory message if `.specify/templates/commands/` is missing. This is intentional. A clear failure is safer than silently generating editor command packs from a nonexistent or partial source.

## Preferred Future Direction

The maintainable target is still:

1. restore a real canonical command source under `.specify/templates/commands/`
2. generate `.cursor/commands/` and `.claude/commands/` from that source
3. keep tool-specific extras such as `.claude/commands/run-caipe-integration-tests.md` outside the shared command-generation path
4. keep root runtime compatibility files separate from contributor-tooling decisions, so future cleanup does not confuse local entrypoints with editor shims

Until that source is restored, treat the checked-in command packs as synced compatibility copies and update them carefully.
