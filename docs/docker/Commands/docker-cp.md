---
id: docker-cp
aliases: []
tags: []
---

# docker cp

Copy files or directories between a container and the host filesystem.

## Syntax

```bash
docker cp CONTAINER:SRC_PATH DEST_PATH
docker cp SRC_PATH CONTAINER:DEST_PATH
```

## Examples

```bash
# Copy from container to host
docker cp mycontainer:/var/log/app.log ./app.log

# Copy from host to container
docker cp ./config.yml mycontainer:/app/config.yml

# Copy a directory
docker cp mycontainer:/app/logs/ ./logs/
```

## Notes

- Works on both running and stopped containers.
- Copies preserve file permissions and timestamps.
- Useful for debugging or extracting data from containers without committing an image.

## Related Notes

- [[Commands/docker-exec|docker exec]]
- [[Commands/docker-commit|docker commit]]
- [[DockerContainer]]
