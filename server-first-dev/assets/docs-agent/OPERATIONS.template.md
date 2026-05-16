# Operations

Commands for **this** deployment. Replace placeholders during bootstrap.

## Inspect

```bash
cd {{PROJECT_ROOT}}
docker compose ps
docker compose logs -f {{SERVICE}}
```

## Build

```bash
# backend
cd {{BACKEND_PATH}} && npm ci && npm run build

# frontend
cd {{FRONTEND_PATH}} && npm ci && npm run build
```

## Deploy / Update

1. Update DEVLOG.md with intent.
2. Pre-deploy DB backup: {{BACKUP_COMMAND}}
3. {{MIGRATE_COMMAND}}
4. {{RESTART_COMMAND}}
5. Verify https://{{PROD_HOST}} and https://{{DEV_HOST}}

## Logs

- App: `docker compose logs {{APP_SERVICE}}`
- Caddy: {{CADDY_LOG_PATH_OR_COMMAND}}

## Debug Checklist

- [ ] Compose services healthy
- [ ] Caddy TLS valid
- [ ] DB reachable from app container
- [ ] MinIO credentials match env
