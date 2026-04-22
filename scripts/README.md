# Scripts Directory

This directory contains utility scripts for the AI Platform Engineering project.

The scripts here are maintenance utilities, test helpers, scanners, and one-off migration tools. They are not the main build or deployment entrypoints for the project.

Use these maintained root entrypoints for normal workflows:

- `docker-compose.yaml`
- `docker-compose.dev.yaml`
- `setup-caipe.sh`
- Helm charts under `charts/`

## Current Script Categories

### Build and Release Helpers

- `generate-helm-chart-docs.sh`: Regenerates Helm chart README files
- `check_pinned_deps.py`: Verifies pinned dependency files stay consistent
- `check_uv_lock_sync.sh`: Checks whether `uv.lock` is in sync
- `add-new-agent-helm-chart.py`: Helper for chart scaffolding

### Streaming and A2A Diagnostics

- `capture_a2a_events.py`
- `compare_a2a_events.py`
- `analyze_a2a_metadata.py`
- `analyze_accumulation_flow.py`
- `trace_a2a_streaming.py`
- `validate_artifacts.py`

These are primarily debugging and evaluation utilities. See the streaming-testing skill docs for guided usage.

### Skills and Content Maintenance

- `scan-packaged-skills.sh`: Runs the packaged-skills scanner
- `cleanup_duplicate_configs.js`: MongoDB cleanup helper for duplicate config docs

### Issue and Migration Utilities

- `sync_beads_to_github.sh`: Sync helper for `bd` / GitHub issue flow
- `migrations/0.3.0/`: One-time migration and backfill scripts for release upgrades

## Removed Dead Workflow

The repository no longer ships the old persona-based `generate-docker-compose.py` workflow. If you see historical references to generated persona-specific compose files, treat them as stale documentation rather than supported build or deploy paths.

For normal local startup and deployment, use the maintained getting-started docs and the root runtime entrypoints instead.
