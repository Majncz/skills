# Development Environment

Two **running** environments on the same server—not just different `.env` files on one process.

## Hostnames

| Environment | Typical hostname | Purpose |
|-------------|------------------|---------|
| Production | `example.com`, `www.example.com` | Live users |
| Development | `dev.example.com` (or user-chosen dev subdomain) | Safe experimentation |

Caddy routes each hostname to the correct Compose service / build.

## Isolation

- Separate PostgreSQL database per environment.
- Separate secrets (workbench can copy between them intentionally).
- Development does **not** need automatic backups by default.
- Do **not** copy production data into development unless the user explicitly asks the AI to do so.

## When To Use Dev

- Testing features before production deploy.
- Showing stakeholders a preview URL.
- Breaking changes without affecting live orders/data.

Document actual hostnames, service names, and DB connection env keys in `docs/agent/ENVIRONMENTS.md` after setup.
