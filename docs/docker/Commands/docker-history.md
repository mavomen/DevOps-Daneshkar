---
id: docker-history
aliases: []
tags: []
---

# docker history

Show the layers of a Docker image and their sizes.

## Syntax

```bash
docker history [OPTIONS] IMAGE
```

## Examples

```bash
# Show all layers
docker history nginx

# Show only size
docker history --format "{{.Size}}" nginx

# Truncate (hide truncated commands)
docker history --no-trunc nginx
```

## Output

Each row shows one layer: the command that created it, who created it, its size, and when.

## Why it matters

- Identify which layer is largest (optimize build).
- See the full command history of an image.
- Useful for debugging bloat in images.

## Related Notes

- [[DockerImage]]
- [[Dockerfile]]
- [[Commands/docker-images|docker images]]
