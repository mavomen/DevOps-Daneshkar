---
id: ComposeNetworking
aliases: []
tags: []
---

# Compose Networking

Docker Compose networking configuration and management.

## Default Behavior

Compose creates a default network for each project. All services in the same `docker-compose.yml` can communicate using service names as hostnames.

## Custom Networks

```yaml
services:
  web:
    networks:
      - frontend
  db:
    networks:
      - backend

networks:
  frontend:
  backend:
```

## Network Drivers

| Driver | Use Case |
|--------|----------|
| `bridge` | Default, single-host communication |
| `overlay` | Multi-host (Swarm) |
| `host` | Use host network stack |
| `none` | Disable networking |

## Related Notes

- [[DockerNetworking]] — Core Docker networking
- [[ComposeCheatsheet]] — Compose command reference
- [[ComposeVolumes]] — Volume management
