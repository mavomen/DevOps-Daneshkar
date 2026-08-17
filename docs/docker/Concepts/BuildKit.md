---
id: BuildKit
aliases: []
tags: []
---

# BuildKit

BuildKit is Docker's modern build engine, replacing the legacy builder. It enables parallel build stages, better caching, and secure secret handling.

## Enable BuildKit

```bash
# Per build
DOCKER_BUILDKIT=1 docker build .

# Globally (daemon.json)
# { "features": { "buildkit": true } }

# Docker Compose
# DOCKER_BUILDKIT=1 docker compose build
```

BuildKit is the default in Docker Desktop and Docker Engine 23.0+.

## Key features

### Parallel stage builds

BuildKit builds independent stages in parallel, not sequentially.

```dockerfile
# These two stages build at the same time
FROM node:20 AS frontend
RUN npm run build

FROM golang:1.22 AS backend
RUN go build -o server .
```

### Build secrets

Mount secrets during build without baking them into layers.

```dockerfile
RUN --mount=type=secret,id=npmrc,target=/root/.npmrc \
    npm ci
```

```bash
docker build --secret id=npmrc,src=.npmrc .
```

### SSH forwarding

Forward SSH agent into the build for private repos.

```dockerfile
RUN --mount=type=ssh \
    git clone git@github.com:private/repo.git
```

```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_rsa
docker build --ssh default .
```

### Cache mounts

Persist directories across builds (npm, pip, go modules).

```dockerfile
RUN --mount=type=cache,target=/root/.cache/pip \
    pip install -r requirements.txt

RUN --mount=type=cache,target=/go/pkg \
    go build -o server .
```

### Cache import/export

Import cache from a previous build or registry.

```bash
docker build \
  --cache-from type=registry,ref=myapp:cache \
  --cache-to type=inline \
  -t myapp:v1 .
```

## When to use

- Multi-stage builds with parallel stages
- Private git repos in Dockerfile
- Faster CI builds with cache mounts
- Secrets that must not persist in image layers

## Related Notes

- [[Dockerfile]]
- [[Commands/docker-build|docker build]]
- [[DockerfileBestPractices]]
- [[MultiStageBuild]]
