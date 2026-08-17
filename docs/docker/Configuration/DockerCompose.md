---
id: DockerCompose
aliases: []
tags: []
---

# Docker Compose

Docker Compose is a tool for defining and running multi-container applications using a YAML file. Instead of running multiple `docker run` commands, you declare everything in one file.

## Install

Docker Compose is included with Docker Desktop. On Linux:

```bash
sudo apt install docker-compose-plugin
```

## docker-compose.yml basics

```yaml
services:
  web:
    image: nginx:alpine
    ports:
      - "8080:80"
    depends_on:
      - app
    networks:
      - frontend

  app:
    build: ./app
    environment:
      - DB_HOST=db
    volumes:
      - app-data:/app/data
    networks:
      - frontend
      - backend

  db:
    image: postgres:16
    environment:
      - POSTGRES_PASSWORD=secret
    volumes:
      - db-data:/var/lib/postgresql/data
    networks:
      - backend

volumes:
  app-data:
  db-data:

networks:
  frontend:
  backend:
```

## Key commands

```bash
# Start all services (detached)
docker compose up -d

# Stop and remove
docker compose down

# View running services
docker compose ps

# View logs
docker compose logs -f

# Rebuild images and start
docker compose up -d --build

# Run a one-off command in a service
docker compose exec app bash
```

## Key concepts

| Concept | Purpose |
|---|---|
| `services` | Define containers to run |
| `volumes` | Named volumes for persistence |
| `networks` | Service-to-service communication |
| `depends_on` | Startup order (not readiness) |
| `build` | Build from a Dockerfile instead of using `image` |
| `environment` | Env vars for a service |
| `ports` | Host-to-container port mapping |

## When to use

- Local development environments (database + app + cache).
- Integration testing with multiple services.
- Any setup where you'd otherwise write a shell script with multiple `docker run` commands.

## Related Notes

- [[Dockerfile]]
- [[Commands/docker-run|docker run]]
- [[Commands/docker-network|docker network]]
- [[Commands/docker-volume|docker volume]]
