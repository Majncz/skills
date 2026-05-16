# Architecture

## Overview

{{WHAT_THE_APP_DOES}}

## Repository Layout

```
{{REPO_TREE_OR_DESCRIPTION}}
```

## Services (Docker Compose)

| Service | Role | Notes |
|---------|------|-------|
| {{SERVICE}} | {{ROLE}} | {{NOTES}} |

## Data Flow

- **API:** Express REST on {{API_PORT_OR_PATH}}
- **Frontend:** Vite React build served by Caddy
- **Database:** PostgreSQL prod `{{PROD_DB}}`, dev `{{DEV_DB}}`
- **Files:** MinIO bucket(s): {{BUCKETS}}
- **Realtime:** Socket.IO on {{WHERE_USED}}

## Workbench

- URL: {{WORKBENCH_URL}}
- Read-mostly ops UI; mutations via AI + documented commands.

## Auth

- JWT in HTTP-only cookie, 90-day expiry
- Admin: {{ONE_PASSWORD_OR_MULTI_USER}}
