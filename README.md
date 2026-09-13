# sandbox-infra

Always-on shared edge for side projects: **Caddy** (TLS + reverse proxy / PHP-FPM).

MySQL is **Aiven** (managed) — not run in this Compose stack.

## Sites

| Host | Backend |
|------|---------|
| `sandbox.didiktrisusanto.dev` | health text |
| `sisbio-new.didiktrisusanto.dev` | Laravel at `/opt/apps/sisbio-new` via host PHP 8.5-FPM |

## Start

1. Origin cert in `caddy/certs/` (must cover `sisbio-new.didiktrisusanto.dev` or `*.didiktrisusanto.dev`)
2. Cloudflare DNS A/AAAA for `sisbio-new` → VPS, proxied
3. Host PHP-FPM running (`php8.5-fpm`), socket `/run/php/php8.5-fpm.sock`
4. Then:

```bash
cd /opt/infra/sandbox-infra
docker compose up -d
```

If Caddy can’t talk to FPM (permission denied on the socket), in the pool config set e.g. `listen.mode = 0666` and reload FPM — Docker’s Caddy user must reach the socket.

Laravel: `APP_URL=https://sisbio-new.didiktrisusanto.dev`, storage writable by the FPM user (`www-data`).

Network name: `sandbox` (external for other Compose files).
