---
id: docker-tag
aliases: []
tags: []
---

# docker tag

Create a new tag for an existing image. Does not create a new image — just an alias.

## Syntax

```bash
docker tag SOURCE_IMAGE[:TAG] TARGET_IMAGE[:TAG]
```

## Examples

```bash
# Tag for Docker Hub
docker tag myapp:v1 myuser/myapp:v1

# Tag for a private registry
docker tag myapp:v1 registry.example.com/myapp:v1

# Tag as latest
docker tag myapp:v1 myapp:latest
```

## Typical workflow

```bash
docker build -t myapp:v1 .
docker tag myapp:v1 myuser/myapp:v1
docker push myuser/myapp:v1
```

## Related Notes

- [[DockerImage]]
- [[Registry]]
- [[Commands/docker-images|docker images]]
