# textbee (Ramtown build): status and handoff

Last updated 2026-11-23 by a Claude Code session on HOME2. This first version comes from the repo's history and workflows. The next session that works here should add what is in progress.
Read this first (global rule 12.1). When you finish, replace stale notes and keep it short.

## What this is

Shul613's fork of textbee.dev, an SMS gateway that sends through an Android phone. The Shul613 box runs its API and its web dashboard (Shul613 `infra/docker-compose.yml`).

## How a change ships

Only one workflow is switched on: `Ramtown release` (`.github/workflows/ramtown-release.yaml`). Upstream's other workflows are off. It runs on a push to main that touches `android/`, `api/`, `web/`, `branding/` or the workflow file itself, and it builds:
- **The Android app,** signed, as a GitHub Release. Obtainium on the office phone installs it.
- **The API and web images,** `ghcr.io/shul-613/textbee/{api,web}:ramtown`. The box's watchtower pulls them in.

The Ramtown branding is applied at build time from `branding/`, so syncing the fork with upstream doesn't conflict.

## State

- **Last change:** 2026-09-10 (branding). The release builds have been green since then.
- **Image owner:** the box reads it as `TEXTBEE_IMAGE_OWNER=shul-613`. The old `ghcr.io/ramtown613` address answers 403.

## Open

- **`ramtown-release.yaml` still uses `actions/checkout@v4` and `setup-java@v4`** (Node 20). They weren't bumped on 2026-11-23, because merging a change to that file rebuilds and ships the phone app and both images. Bump them with the next real release.
