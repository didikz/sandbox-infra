# sandbox-infra

Always-on shared stack for side projects: **Caddy** + **MySQL**.

Postgres and Redis can be added later when a project needs them.

## Start

```bash
cd ~/Code/sandbox-infra
cp .env.example .env   # if needed
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

Create extra DBs once infra is up:

```bash
docker compose exec mysql mysql -usandbox -psandbox -e 'CREATE DATABASE myapp;'
```

Or drop SQL into `mysql/init/` before first boot.

## Host access

MySQL is also on localhost for tools outside Docker: `127.0.0.1:3306`
