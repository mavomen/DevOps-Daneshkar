---
id: DockerComposeCheatsheet
aliases: []
tags: []
---

# Docker Compose Cheatsheet

Quick reference for docker compose commands.

## Service Management

```bash
docker compose up -d                            # Start services detached
docker compose down                             # Stop and remove services
docker compose start                            # Start stopped services
docker compose stop                             # Stop running services
docker compose restart                          # Restart services
docker compose ps                               # List services
docker compose logs -f                          # Follow service logs
docker compose logs web                         # Logs for specific service
```

## Building and Rebuilding

```bash
docker compose build                            # Build all services
docker compose build web                        # Build specific service
docker compose up --build                       # Rebuild and start
docker compose pull                             # Pull latest images
```

## Executing Commands

```bash
docker compose exec web bash                    # Shell into service
docker compose exec web python manage.py migrate # Run command in service
docker compose run web pytest                   # Run one-off command
docker compose run --rm web python script.py    # Run and remove container
```

## Volume and Network

```bash
docker compose up -d --force-recreate           # Recreate containers
docker compose down -v                          # Remove volumes too
docker compose down --rmi all                   # Remove images too
docker compose config                           # Validate and view config
```

## Common Compose File

```yaml
services:
  web:
    build: .
    ports:
      - "8080:80"
    environment:
      - DATABASE_URL=postgres://db:5432/mydb
    depends_on:
      - db
    volumes:
      - ./app:/app
    restart: unless-stopped

  db:
    image: postgres:16
    environment:
      POSTGRES_PASSWORD: secret
    volumes:
      - pgdata:/var/lib/postgresql/data

volumes:
  pgdata:
```

## Related Notes

- [[ComposeNetworking]] - Network configuration
- [[ComposeVolumes]] - Volume management
- [[ComposeProfiles]] - Profile usage
