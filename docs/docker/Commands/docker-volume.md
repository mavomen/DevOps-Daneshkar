---
id: docker-volume
aliases: []
tags: []
---

# docker volume

Manage Docker volumes for persistent data storage.

## Why volumes

Data inside a container is lost when the container is removed. Volumes persist data on the host, independent of the container lifecycle.

```
Container deleted → Container's data lost → Volume data remains
```

## Create a volume

```bash
docker volume create mydata
```

## Use a volume

```bash
# Mount by name
docker run -d --name myapp -v mydata:/app/data nginx

# Read-only mount
docker run -d -v mydata:/app/data:ro nginx

# Bind mount (host directory)
docker run -d -v /host/path:/container/path nginx
```

## Manage volumes

```bash
# List volumes
docker volume ls

# Inspect volume details
docker volume inspect mydata

# Remove unused volumes
docker volume prune

# Remove specific volume
docker volume rm mydata
```

## Named vs anonymous vs bind mounts

| Type | Example | Persistence |
|---|---|---|
| Named | `-v mydata:/app/data` | Survives container removal |
| Anonymous | `-v /app/data` | Orphaned on removal |
| Bind mount | `-v /host/path:/app/path` | Host-managed |

## Related Notes

- [[DockerContainer]]
- [[Commands/docker-run|docker run]]
- [[Commands/docker-prune|docker prune]]
