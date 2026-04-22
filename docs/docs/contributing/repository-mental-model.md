# Repository Mental Model

This page is the quick orientation guide for contributors who need to understand the CAIPE repository before changing code, docs, or deployment assets.

## What This Repository Is

`ai-platform-engineering` is the CAIPE application repository. It contains the product code, local runtime entrypoints, UI, Helm charts, tests, and the documentation site.

This repository is not the same thing as `stacks`, and it is not the same thing as `idpbuilder`.

## What Belongs Where

### Product Code and Runtime Surface

These are the parts that define the CAIPE application itself:

- `ai_platform_engineering/`: Python backend, agents, orchestration, MCP integrations, shared utilities
- `ui/`: Next.js frontend
- `charts/`: Helm charts for deploying CAIPE and RAG components
- `docker-compose.yaml`, `docker-compose.dev.yaml`, `.env.example`: local runtime entrypoints and configuration examples
- `tests/`, `integration/`: automated test coverage
- `docs/`: Docusaurus site for user, operator, and contributor documentation

### Deployment and Bootstrap Code

These support running or packaging CAIPE, but they are not the application itself:

- `stacks`: a separate repository of `idpbuilder` packages and reference environments
- `idpbuilder`: an external CLI used to stand up local platform environments
- `deploy/`: example manifests, secret examples, and local bootstrap assets
- `build/`: Dockerfiles and image build entrypoints

### Contributor Tooling

These files help contributors and AI-assisted workflows, but they are not product surface:

- `AGENTS.md`
- `CLAUDE.md`
- `.claude/`
- `.cursor/`
- `.specify/`
- `skills/`
- `.beads/`

If these files stay in the repository root, they should be documented as contributor tooling rather than treated as part of the application architecture.

For contributor-tooling maintenance details, see [Contributor Tooling](./contributor-tooling.md).

### Root Runtime Compatibility Files

Some root-level files look similar to contributor tooling but actually exist to support local runtime and compatibility workflows:

- `prompt_config.yaml`, `task_config.yaml`, `policy.lp`: root symlinks to chart data used by compose, UI/API fallbacks, and local compatibility paths
- `persona.yaml`: source data for compose-generation scripts
- `slim-config.yaml`: local SLIM transport config used by compose and workshop flows

These files may still deserve future cleanup, but they should be treated as runtime entrypoints first, not as editor-tooling clutter.

## Recommended Local Layout

The cleanest local layout is to keep `ai-platform-engineering` and `stacks` as sibling checkouts:

```text
workspace/
  ai-platform-engineering/
  stacks/
```

Keeping `stacks` nested inside the app repo makes `git status` harder to read and hides the fact that it is a separate Git repository with its own lifecycle.

If you temporarily keep a `stacks/` checkout inside this repository, the outer repo should ignore that directory so local bootstrap work does not look like CAIPE app changes.

## Current Housekeeping Baseline (2026-04-21)

This baseline was captured after protecting the live worktree on local safety branches and fetching the latest upstream `main` branches.

### Ahead and Behind

- Outer repo: `0` commits ahead, `9` commits behind `origin/main`
- `stacks`: `0` commits ahead, `0` commits behind `origin/main`

### Upstream Drift in the Outer Repo

The outer repo is behind upstream mainly in:

- GitHub Actions and release workflows
- Helm chart version and template updates
- dependency metadata in `pyproject.toml` and `uv.lock`
- single-node chart and service account changes

### Local-Only Docs and Config Drift

Current local-only docs or config changes include:

- `docs/docs/getting-started/idpbuilder/setup.md`
- `.env.example`

These are good candidates for small, safe cleanup because they change repo narrative more than runtime behavior.

### Local-Only Deployment and Runtime Drift

Current local-only deployment or runtime changes include:

- outer repo: `docker-compose.yaml`, `docker-compose.dev.yaml`, `deep_agent.py`, `protocol_bindings/a2a/agent.py`, `middleware.py`
- `stacks`: CAIPE base manifests, setup scripts, workshop values, Keycloak manifests
- untracked `stacks` files: `TROUBLESHOOTING.md`, `caipe/scripts/sync-local-to-gitea.sh`

## Housekeeping Rules for Small Safe Changes

- Keep the root focused on real entrypoints, governance files, and top-level project surfaces.
- Put deeper repository-structure guidance in contributor docs, not in the user-facing README.
- Prefer clarifying ownership and documentation before moving files.
- Treat `stacks` as external packaging and deployment context, not as a subdirectory of the CAIPE app.
- Audit references before moving root config such as `persona.yaml`, `prompt_config.yaml`, `task_config.yaml`, `slim-config.yaml`, or `policy.lp`.

## Near-Term Cleanup Direction

The next safe improvements should stay narrow:

- keep upstream references canonical in docs
- reduce placeholder documentation that adds noise without adding decisions
- document contributor tooling clearly
- avoid broad refactors until the repo story is easier to explain
