---
id: docker-prune
aliases: []
tags: []
---

# docker prune

Remove unused Docker resources to free disk space.

## Prune by type

```bash
# Stopped containers
docker container prune

# Dangling images (untagged, not referenced)
docker image prune

# Unused volumes
docker volume prune

# Unused networks
docker network prune

# Everything at once
docker system prune
```

## system prune details

`docker system prune` removes:
- Stopped containers
- Unused networks
- Dangling images
- Build cache

```bash
# Include volumes in system prune
docker system prune --volumes
```

## Dry run

```bash
# See what would be removed without actually removing
docker system prune --filter "until=24h"
```

## When to use

- Disk space is running low.
- After a build-heavy session (dangling images pile up).
- Periodic cleanup in CI/CD environments.

## Related Notes

- [[Commands/docker-images|docker images]]
- [[Commands/docker-ps|docker ps]]
- [[Commands/docker-volume|docker volume]]
