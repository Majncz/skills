# Backups And Rollback

## Philosophy

The AI has broad server access—make changes **reversible** and **visible**. Workbench shows status; **AI performs restore**, not dangerous one-click restore buttons.

## Backup Levels

### Level 1 — Local (required for first ship)

- No external service setup required.
- Store on server in a dedicated backup area (and/or MinIO backup bucket):
  - Production PostgreSQL dumps (scheduled).
  - MinIO bucket data if uploads exist.
  - Optional config snapshots (Compose, Caddy paths—no secret values in plain text).
- Show status and restore point list in workbench.

**Retention (default policy):**

- Hourly backups for the last **24 hours**.
- After 24 hours, keep **one backup per day**.
- Beyond that: prune based on disk space and app importance; document choice in `docs/agent/BACKUPS.md`.

Warn users: local-only backups do **not** protect against total server loss.

### Level 2 — Hetzner Storage Box (recommended upgrade)

- User connects Storage Box later.
- Encrypted copies of dumps and important files off-server.
- Readiness item: configured or explicitly deferred.

### Level 3 — Point-in-time recovery (out of scope v1)

PostgreSQL PITR (WAL-G, pgBackRest) is possible but too complex for the article workflow. Do not implement unless user explicitly asks for advanced setup.

## What To Back Up

| Asset | Method |
|-------|--------|
| Code | Git + GitHub (readiness step) |
| Database | `pg_dump` scheduled + pre-deploy |
| Uploads | MinIO data copy |
| Secrets | Encrypted export or regeneration docs |
| Workbench state | DB or files as implemented |

## Pre-Deploy Checkpoint

Before migrations or risky deploys: run a production DB dump and note the filename in `DEVLOG.md`.

## Rollback

User may say: "roll back to yesterday" or "undo last deploy."

Support via:

1. **Code:** `git checkout` / revert commit (GitHub remote).
2. **Database:** restore from named dump (document steps in `docs/agent/ROLLBACK.md`).
3. **Files:** restore MinIO backup if applicable.
4. **Config:** DEVLOG + deployment notes.

Update `docs/agent/ROLLBACK.md` with project-specific commands after bootstrap. Keep it honest about what was tested vs assumed.

## GitHub

Connection is a **readiness step before** treating off-server backup as done. Guide SSH key and repo setup if user opts in; see workbench-readiness-checklist.

## Scripts

Do not ship brittle one-size-fits-all backup scripts in the skill. Create/adapt cron or Compose sidecars at runtime and document them in `OPERATIONS.md`.
