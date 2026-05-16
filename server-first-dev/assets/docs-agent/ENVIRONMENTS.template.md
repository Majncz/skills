# Environments

## Hostnames

| Env | URL | Compose service(s) |
|-----|-----|-------------------|
| Production | https://{{PROD_HOST}} | {{PROD_SERVICES}} |
| Development | https://{{DEV_HOST}} | {{DEV_SERVICES}} |

## Secret Names (values not stored here)

| Name | Production | Development |
|------|------------|-------------|
| DATABASE_URL | yes | yes |
| JWT_SECRET | yes | yes |
| MINIO_* | {{}} | {{}} |
| SMTP_* | {{}} | {{}} |

Manage values in the **server workbench** secrets UI.

## Databases

- Prod: `{{PROD_DB_NAME}}`
- Dev: `{{DEV_DB_NAME}}`

Do not copy prod data to dev unless the user explicitly requests it.
