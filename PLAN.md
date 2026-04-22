# Housekeeping Plan

This temporary plan tracks lean housekeeping work in the private fork while the repository is being simplified.

It is not a permanent steering document. Shared repo policy lives in `AGENTS.md`.

## Operating Rules

- Keep changes small, reversible, and easy to explain.
- Do not refactor product functionality as part of housekeeping.
- Do not move files in bulk before ownership is documented.
- Keep one shared AI-development steering document: `AGENTS.md`.
- Reduce tool-specific wrappers instead of expanding them.

## Completed

- protected the original working state on safety branches
- fetched upstream and documented drift
- added contributor mental-model docs
- canonicalized active `stacks` references in docs
- removed unused root Node package files
- removed dead persona-based compose-generator workflow and stale references
- clarified contributor command-pack ownership
- ignored nested `stacks/` checkout noise
- classified root tooling vs runtime compatibility files
- collapsed `CLAUDE.md` into a thin compatibility wrapper
- collapsed `.cursorrules` into a thin compatibility wrapper
- collapsed `.cursor/rules/specify-rules.mdc` into a thin compatibility rule

## Next Small Steps

### 1. Finish Root Tooling Audit

- audit `.claude/commands/` and `.cursor/commands/` for dead or obsolete command files
- decide whether checked-in command packs should stay as synced compatibility copies or move toward one canonical source later

### 2. Reduce Root Cognitive Load Further

- audit remaining root files and folders by category: keep, document, move later, or remove
- identify placeholder, dead, or low-value files that are not runtime entrypoints
- avoid deleting runtime compatibility files such as `prompt_config.yaml`, `task_config.yaml`, `policy.lp`, and `slim-config.yaml` until references are simplified

### 3. Organize Scattered Docs and Scripts

- audit `scripts/` for dead, one-off, or undocumented utilities
- audit scattered Markdown outside `docs/` for overlap, placeholder content, or stale guidance
- consolidate narrative docs by linking or absorbing low-value fragments before moving files

### 4. Prepare a Lean Target Layout

- keep root focused on entrypoints, governance, and minimal compatibility wrappers
- treat `stacks` as a sibling checkout, not part of the app tree
- keep product code, deployment/bootstrap assets, and contributor tooling clearly separated
- propose moves only after each candidate is proven safe by reference audit
