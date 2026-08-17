---
id: LocalDevEnvironment
aliases: []
tags: []
---

# Local Development Environment

Using Docker Compose for local development with hot-reload, service dependencies, and dev-specific overrides.

## Base compose file

```yaml
# docker-compose.yml
services:
  app:
    build: .
    ports:
      - "3000:3000"
    depends_on:
      db:
        condition: service_healthy
    environment:
      - DB_HOST=db
      - DB_PORT=5432

  db:
    image: postgres:16
    environment:
      - POSTGRES_PASSWORD=devpassword
    volumes:
      - pgdata:/var/lib/postgresql/data
    healthcheck:
      test: ["CMD-SHELL", "pg_isready -U postgres"]
      interval: 5s
      timeout: 5s
      retries: 5

volumes:
  pgdata:
```

## Dev override with bind mounts

```yaml
# docker-compose.override.yml (auto-loaded)
services:
  app:
    volumes:
      - ./src:/app/src    # hot-reload: edit on host, see changes instantly
    environment:
      - NODE_ENV=development
      - DEBUG=*
```

```bash
# Just works — override is auto-applied
docker compose up -d
```

## Hot-reload examples

| Language | Add to volumes |
|---|---|
| Node.js | `- ./src:/app/src` + nodemon |
| Python | `- ./app:/app` + flask run --reload |
| Go | `- ./cmd:/app/cmd` + air |
| Java | Not suitable for bind mounts (use rebuild) |

## Dev workflow

```bash
# Start everything
docker compose up -d

# Follow logs
docker compose logs -f app

# Open a shell in the running app
docker compose exec app bash

# Rebuild after Dockerfile changes
docker compose up -d --build

# Tear down everything (including volumes)
docker compose down -v
```

## Separate profiles for optional services

```yaml
services:
  app:
    build: .
    profiles: ["dev"]

  debug-tools:
    image: busybox
    profiles: ["debug"]
```

```bash
docker compose --profile dev --profile debug up -d
```

## Common pitfalls

- **Bind mount + container restart**: Changes persist because they're on the host.
- **Database in containers**: Use named volumes, not bind mounts, for data.
- **Port conflicts**: Ensure host ports are free or change mappings.

## Related Notes

- [[DockerCompose]]
- [[ComposeProfiles]]
- [[Commands/docker-volume|docker volume]]
