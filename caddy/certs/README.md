# Cloudflare Origin Certificate

Do not commit `origin.pem` / `origin.key`.

1. Cloudflare dashboard → **SSL/TLS** → **Origin Server** → **Create certificate**
2. Hostnames: `sandbox.didiktrisusanto.dev` (add `*.didiktrisusanto.dev` if you want one cert for more apps)
3. Leave private key type default (RSA)
4. Create → copy **Origin Certificate** → save as `origin.pem`
5. Copy **Private Key** → save as `origin.key`
6. Zone **SSL/TLS** mode: **Full** or **Full (strict)** (Origin CA works with both)
7. On the VPS: `docker compose up -d` (or recreate caddy)

```bash
chmod 600 origin.key
chmod 644 origin.pem
```
