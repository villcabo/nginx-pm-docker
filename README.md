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

## Using PostgreSQL

Uncomment `COMPOSE_FILE` in your `.env`:

```env
COMPOSE_FILE=docker-compose.yml:docker-compose.postgres.yml
```

### Local Postgres (container)

Activate the `local-db` profile:

```env
COMPOSE_PROFILES=local-db
DB_HOST=database
```

```bash
docker compose up -d
```

### External Postgres

Leave the profile empty and point `DB_HOST` to your server:

```env
#COMPOSE_PROFILES=
DB_HOST=db.example.com
DB_PORT=5432
DB_USER=npm
DB_NAME=npm
DB_PASS=yourpassword
```

```bash
docker compose up -d
```

## Networks

- `nginx-pm-network`: internal (NPM ↔ DB).
- `nginx-pm-router`: external — attach any container you want NPM to proxy.

MTU is configurable via `NETWORK_MTU` in `.env`.

### Connecting an external container

To let NPM reach a container by name, attach it to `nginx-pm-router` — either
in its own compose file as an external network:

```yaml
networks:
  nginx-pm-router:
    external: true
```

or on the fly:

```bash
docker network connect nginx-pm-router <container>
```

## Default credentials

```
username: admin@example.com
password: changeme
```
