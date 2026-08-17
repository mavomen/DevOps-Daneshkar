---
id: docker-images
aliases: []
tags: []
---

# docker images

List all images stored on the local system.

## Syntax

```bash
docker images [OPTIONS] [REPOSITORY[:TAG]]
```

## Examples

```bash
# List all images
docker images

# Filter by repository
docker images nginx

# Show image IDs only
docker images -q

# Show dangling images only
docker images -f "dangling=true"
```

## Output columns

| Column | Meaning |
|---|---|
| REPOSITORY | Image name |
| TAG | Version tag |
| IMAGE ID | Short SHA |
| CREATED | When the image was built |
| SIZE | Disk usage |

## Related Notes

- [[DockerImage]]
- [[Commands/docker-pull|docker pull]]
- [[Commands/docker-build|docker build]]
- [[Commands/docker-rm|docker rm]]
