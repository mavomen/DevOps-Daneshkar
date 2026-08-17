---
id: docker-build
aliases: []
tags: []
---

# docker build

Build a Docker image from a Dockerfile and a build context.

## Syntax

```bash
docker build [OPTIONS] PATH | URL | -
```

## Common options

| Option | Purpose |
|---|---|
| `-t name:tag` | Name and tag the image |
| `--build-arg KEY=VAL` | Pass build-time variables |
| `-f Dockerfile` | Specify Dockerfile path |
| `--no-cache` | Build without using cache |
| `--target stage` | Build up to a specific stage (multi-stage) |

## Examples

```bash
# Build from current directory
docker build -t myapp:v1 .

# Use a specific Dockerfile
docker build -f Dockerfile.prod -t myapp:prod .

# Pass build argument
docker build --build-arg VERSION=2.0 -t myapp:v2 .

# No cache
docker build --no-cache -t myapp:v1 .
```

## Build context

The `.` in `docker build .` is the build context — all files in that directory are sent to the daemon. Use `.dockerignore` to exclude files.

## Related Notes

- [[Dockerfile]]
- [[DockerImage]]
- [[Commands/docker-images|docker images]]
- [[DockerfileBestPractices]]
