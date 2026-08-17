---
id: ComposeVolumes
aliases: []
tags: []
---

# Compose Volumes

Docker Compose volume configuration for persistent data.

## Volume Types

| Type | Syntax | Purpose |
|------|--------|---------|
| Named volume | `volumes: - mydata:/app/data` | Persistent data |
| Bind mount | `volumes: - ./src:/app` | Development sync |
| tmpfs | `tmpfs: /tmp` | Ephemeral data |

## Syntax

```yaml
services:
  db:
    volumes:
      - pgdata:/var/lib/postgresql/data  # Named volume
      - ./init.sql:/docker-entrypoint-initdb.d/init.sql  # Bind mount

volumes:
  pgdata:
```

## Commands

```bash
docker compose up -d                    # Create volumes
docker compose down -v                  # Remove volumes
docker volume ls                        # List all volumes
docker volume inspect <volume-name>     # Volume details
```

## Related Notes

- [[ComposeNetworking]] — Network configuration
- [[ComposeCheatsheet]] — Compose command reference
- [[ComposeProfiles]] — Profile usage
