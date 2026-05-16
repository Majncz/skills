# Backups

## Policy

- **Level 1 (active):** local backups on server at `{{BACKUP_PATH}}`
- **Retention:** hourly for 24h, then one per day
- **Level 2:** Hetzner Storage Box — {{CONFIGURED_OR_DEFERRED}}

## Risk

Local-only backups do **not** survive total server loss. Enable Storage Box for production-critical data.

## What Is Backed Up

- [ ] Production PostgreSQL (`pg_dump`)
- [ ] MinIO buckets: {{LIST}}
- [ ] Code: Git remote {{GITHUB_URL_OR_NONE}}

## Schedule

- Cron / sidecar: {{HOW_SCHEDULED}}
- Last successful backup: check workbench or `{{LIST_COMMAND}}`

## Restore

Restores are performed by the AI using steps in [ROLLBACK.md](ROLLBACK.md). Do not use undocumented manual steps on production without a DEVLOG entry.
