---
id: ComposeProfiles
aliases: []
tags: []
---

# Compose Profiles

Profiles let you selectively start groups of services. Only services in active profiles (or services with no profile) start by default.

## Define profiles

```yaml
services:
  web:
    image: nginx
    # No profile → always starts

  app:
    build: ./app
    profiles: ["dev", "debug"]

  db:
    image: postgres:16
    profiles: ["dev"]

  debug-tools:
    image: busybox
    profiles: ["debug"]
```

## Start with profiles

```bash
# Default only (web starts, everything else skipped)
docker compose up -d

# Dev environment (web + app + db)
docker compose --profile dev up -d

# Debug environment (web + app + debug-tools)
docker compose --profile debug up -d

# Multiple profiles
docker compose --profile dev --profile debug up -d
```

## depends_on with conditions

```yaml
services:
  app:
    build: ./app
    depends_on:
      db:
        condition: service_healthy
      redis:
        condition: service_started

  db:
    image: postgres:16
    healthcheck:
      test: ["CMD-SHELL", "pg_isready -U postgres"]
      interval: 5s
      timeout: 5s
      retries: 5

  redis:
    image: redis:alpine
```

## Compose files structure

```yaml
# docker-compose.yml (base)
services:
  web:
    image: nginx

# docker-compose.override.yml (auto-loaded)
services:
  web:
    volumes:
      - ./html:/usr/share/nginx/html

# docker-compose.prod.yml (explicit)
services:
  web:
    restart: always
    logging:
      driver: json-file
      options:
        max-size: "10m"
```

```bash
# Base + override loaded automatically
docker compose up

# Base + prod (override ignored)
docker compose -f docker-compose.yml -f docker-compose.prod.yml up
```

## Key commands

```bash
# View resolved config
docker compose config

# List profiles
docker compose profiles

# Dry run (validate without starting)
docker compose --dry-run up
```

## When to use profiles

- Separate dev/test/prod service sets
- Optional services (monitoring, debug tools, workers)
- Avoid starting everything in every environment

## Related Notes

- [[DockerCompose]]
- [[DaemonConfiguration]]
- [[DockerContainer]]
