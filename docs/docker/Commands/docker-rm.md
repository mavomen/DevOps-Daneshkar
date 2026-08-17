---
id: docker-rm
aliases: []
tags: []
---

# docker rm

Remove one or more stopped containers.

## Syntax

```bash
docker rm [OPTIONS] CONTAINER [CONTAINER...]
```

## Examples

```bash
# Remove a stopped container
docker rm <container>

# Force remove (even if running)
docker rm -f <container>

# Remove all stopped containers
docker rm $(docker ps -aq)

# Remove container and its volumes
docker rm -v <container>
```

## Common pattern: clean up everything

```bash
# Stop and remove all containers
docker rm -f $(docker ps -aq)
```

## Notes

- `docker rm` only removes **stopped** containers by default.
- Use `-f` to force-remove a running container (sends SIGKILL).
- Use `docker stop` first for graceful shutdown.

## Related Notes

- [[Commands/docker-ps|docker ps]]
- [[Commands/docker-run|docker run]]
- [[DockerContainer]]
