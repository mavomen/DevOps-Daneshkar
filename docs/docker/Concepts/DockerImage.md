---
id: DockerImage
aliases: []
tags: []
---

# Docker Image

A Docker image is a read-only template created from a Dockerfile. It contains everything needed to run an application: code, runtime, libraries, environment variables, and configuration.

## Key properties

- **Immutable** — once built, an image never changes.
- **Layered** — each Dockerfile instruction creates a new layer. Layers are cached and shared between images.
- **Tagged** — identified by name and tag (`nginx:alpine`, `python:3.12`). Default tag is `latest`.

## Image vs Container

| Image | Container |
|---|---|
| Read-only template | Running (writable) instance |
| Blueprint | Built house |
| Created with `docker build` | Created with `docker run` |
| Stored on disk / registry | Running in memory |

## Create images

```bash
# From a Dockerfile
docker build -t myapp:v1 .

# From a running container
docker commit <container_id> myapp:v1
```

## Inspect images

```bash
docker images              # list all images
docker image inspect <id>  # detailed metadata
docker history <image>     # show layers and sizes
```

## Related Notes

- [[WhatIsDocker]]
- [[DockerContainer]]
- [[Dockerfile]]
- [[Commands/docker-build|docker build]]
- [[Commands/docker-images|docker images]]
- [[Commands/docker-commit|docker commit]]
