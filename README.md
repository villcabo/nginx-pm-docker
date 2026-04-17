# Nginx Proxy Manager

Docker Compose setup for [Nginx Proxy Manager](https://nginxproxymanager.com/).

## Quick start

```bash
git clone https://github.com/villcabo/nginx-pm-docker.git
cd nginx-pm-docker
cp .env.example .env
docker compose up -d
```

By default it runs with **SQLite** (embedded, no extra service).

## Using PostgreSQL (optional)

Uncomment `COMPOSE_FILE` in your `.env`:

```env
COMPOSE_FILE=docker-compose.yml:docker-compose.postgres.yml
```

Then:

```bash
docker compose up -d
```

This starts a PostgreSQL container and wires NPM to it via `DB_POSTGRES_*` environment variables.

## Default credentials

```
username: admin@example.com
password: changeme
```
