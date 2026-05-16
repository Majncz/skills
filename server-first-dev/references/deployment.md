# Deployment

Target: single **Hetzner Ubuntu** server. User has already connected via SSH before this skill runs.

## Components

- **Caddy:** reverse proxy, automatic HTTPS, serve built frontend, proxy API.
- **Docker Compose:** app (prod + dev), PostgreSQL (prod + dev), MinIO, workbench, supporting services as needed.
- **Domain:** A records for `example.com` and `www`; dev subdomain per [development-environment.md](development-environment.md).

Exact Compose service names, networks, and volume paths are **not** fixed in this skill—choose a clear layout and document it in `docs/agent/ARCHITECTURE.md` and `ENVIRONMENTS.md`.

## Deploy / Update Flow

Each deployment should:

1. Record intent in `docs/agent/DEVLOG.md`.
2. Commit or tag code if using Git.
3. Run `pg_dump` (or project backup hook) before risky migrations.
4. Install dependencies, build frontend, run Prisma migrations.
5. Restart affected Compose services.
6. Verify prod (and dev if changed) reachable.
7. Update workbench readiness if applicable.

Provide a simple script or documented commands in `docs/agent/OPERATIONS.md`—adapt to the repo you created.

## Static Assets And Uploads

- Built frontend: Caddy static file route or equivalent.
- User uploads: MinIO buckets; never mix upload paths with app source.

## Firewall / Deploy User

Not a focus of bootstrap. Set basics only if obviously needed; do not block shipping the app on hardening polish.

## Hetzner Server Backups

Mention that Hetzner snapshot backups are a blunt whole-server safety net—not a substitute for app-level backups in [backups-and-rollback.md](backups-and-rollback.md).
