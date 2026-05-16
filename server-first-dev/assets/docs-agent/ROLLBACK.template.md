# Rollback

## When To Use

- Bad deploy, broken migration, accidental data change
- User asks to "go back" to a previous version

## Code

```bash
cd {{PROJECT_ROOT}}
git log --oneline -20
git checkout {{COMMIT_OR_TAG}}  # or git revert
{{REBUILD_AND_RESTART}}
```

## Database

1. Identify dump file from workbench or `{{BACKUP_PATH}}`
2. Stop app or put in maintenance if needed
3. Restore: {{RESTORE_COMMAND_FOR_THIS_PROJECT}}
4. Verify app health; update DEVLOG.md

## Files (MinIO)

{{MINIO_RESTORE_STEPS}}

## After Rollback

- Document what was restored and why in DEVLOG.md
- Update READINESS.md if checklist items affected

## Limits

Point-in-time recovery (WAL/PITR) is **not** configured unless explicitly documented here.
