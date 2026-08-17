---
id: docker-pull
aliases: []
tags: []
---

# docker pull

Download an image from a registry (Docker Hub by default).

## Syntax

```bash
docker pull [OPTIONS] NAME[:TAG|@DIGEST]
```

## Examples

```bash
# Pull latest version
docker pull nginx

# Pull specific version
docker pull nginx:alpine

# Pull from a specific registry
docker pull registry.example.com/myapp:v1
```

## Notes

- `docker run` automatically pulls if the image is not found locally.
- Images are pulled layer by layer — cached layers are reused.
- Use `docker image prune` to remove dangling (untagged) images after pulling newer versions.

## Related Notes

- [[Commands/docker-run|docker run]]
- [[Commands/docker-images|docker images]]
- [[Registry]]
