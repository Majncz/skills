# Technology Decisions

Defaults for server-first projects. Deviate only when the user or app clearly requires it.

## Stack

| Layer | Choice | Notes |
|-------|--------|-------|
| Runtime | Node.js latest stable LTS | |
| Language | TypeScript strict | |
| Package manager | npm | Universal on fresh servers |
| Backend | Express.js | Fastify is a valid alternative, not default |
| API | REST | Resource-oriented routes |
| ORM | Prisma | Migrations on deploy |
| Database | PostgreSQL latest stable in Docker | Separate DB per environment |
| Frontend | React + Vite | Built assets served via Caddy |
| Reverse proxy | Caddy | Automatic HTTPS |
| Process orchestration | Docker Compose | Service layout: decide at runtime |
| Realtime | Socket.IO | See policy below |
| Object storage | MinIO (S3-compatible) | Uploads, file backups when used |
| Email | Nodemailer + SMTP + MJML + text fallback | |
| Auth | JWT 90-day, HTTP-only cookie | bcrypt if passwords stored |
| Admin UI | shadcn/ui + lucide-react | See admin-design reference |
| Public UI | Distinctive custom design | See frontend-design reference |
| Validation | Zod | API, env, forms |
| Admin forms | React Hook Form + Zod | |
| Payments | User-provided | Not in core skill |

## Realtime Policy

Use Socket.IO (not polling) when:

- Admin or internal screens show changing data.
- Order dashboards or order status/confirmation pages need live updates.

Do **not** use sockets on static presentation pages (e.g. restaurant homepage)—unnecessary load.

## Structure

- Monorepo; agent chooses folder layout.
- Separate frontend/backend processes in Compose; Caddy serves static frontend.
- Shared types: only when they reduce duplication without ceremony.

## Logging And Errors

- Logs on server, inspectable by AI (files, `docker compose logs`, journal).
- No Sentry or similar by default.
- User-facing errors must be specific and actionable, especially in admin.

## Security Baseline

HTTPS only; rate-limit login and sensitive forms; protect `/admin` and workbench routes; validate input; safe upload limits for MinIO.
