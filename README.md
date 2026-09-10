# sandbox-infra

Always-on shared stack for side projects: **Caddy** + **MySQL**.

Caddy terminates TLS with a **Cloudflare Origin Certificate** so the zone can stay on **Full** / **Full (strict)**.

Postgres and Redis can be added later when a project needs them.

## Start

1. Put Origin cert files in `caddy/certs/` (see `caddy/certs/README.md`)
2. Then:

```bash
cd /opt/infra/sandbox-infra   # or ~/Code/sandbox-infra
cp .env.example .env          # if needed
docker compose up -d
```

Network name: `sandbox` (external for other Compose files).

## From another project

```yaml
services:
  app:
    # ...
    networks:
      - sandbox
    environment:
      DATABASE_URL: mysql://sandbox:sandbox@mysql:3306/myapp

networks:
  sandbox:
    external: true
```

## Host access

MySQL on localhost: `127.0.0.1:3306`
