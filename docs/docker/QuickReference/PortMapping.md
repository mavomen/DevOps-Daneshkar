---
id: DockerPortMapping
aliases: []
tags: []
---

# Docker Port Mapping

Quick reference for container port mapping.

## Basic Syntax

```bash
docker run -p HOST:CONTAINER image              # Map host port to container port
docker run -p 8080:80 nginx                     # Host 8080 → Container 80
docker run -p 127.0.0.1:8080:80 nginx           # Bind to localhost only
docker run -p 8080:80/udp nginx                 # UDP mapping
docker run -P nginx                             # Map all exposed ports to random host ports
```

## Common Patterns

| Host Port | Container Port | Use Case |
|-----------|----------------|----------|
| `8080:80` | Web server | Development |
| `3306:3306` | MySQL | Database access |
| `5432:5432` | PostgreSQL | Database access |
| `6379:6379` | Redis | Cache access |
| `0.0.0.0:8080:80` | Web server | All interfaces |

## Docker Compose

```yaml
services:
  web:
    image: nginx
    ports:
      - "8080:80"           # Host:Container
      - "127.0.0.1:8443:443"  # Bind to localhost
      - "9090:9090/udp"     # UDP mapping
```

## Related Notes

- [[DockerNetworking]] - Network configuration
- [[ComposeNetworking]] - Compose network setup
- [[ContainerLifecycle]] - Container states
