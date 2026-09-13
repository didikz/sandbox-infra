# sandbox-infra

Always-on shared edge for side projects: **Caddy** (TLS + reverse proxy).

MySQL is **Aiven** (managed) — not run in this Compose stack.

Caddy terminates TLS with a **Cloudflare Origin Certificate** so the zone can stay on **Full** / **Full (strict)**.

Postgres / Redis can be added later if you need them on the VPS.

## Start

1. Put Origin cert files in `caddy/certs/` (see `caddy/certs/README.md`)
2. Then:

```bash
cd /opt/infra/sandbox-infra   # or ~/Code/sandbox-infra
docker compose up -d
```

Network name: `sandbox` (external for other Compose files).

## From another project

Join the `sandbox` network for Caddy routing; point `DB_*` at your Aiven MySQL URL.

```yaml
services:
  app:
    # ...
    networks:
      - sandbox
    environment:
      DATABASE_URL: mysql://USER:PASSWORD@YOUR_AIVEN_HOST:PORT/DB?ssl-mode=REQUIRED

networks:
  sandbox:
    external: true
```

Add a Caddy site block per app subdomain (`myapp.didiktrisusanto.dev` → `reverse_proxy app:PORT`).
