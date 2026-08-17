---
id: ImageBuilding
aliases: []
tags: []
---

# Image Building

Building Docker images from Dockerfiles.

## Build Command

```bash
docker build -t myapp:v1 .              # Basic build
docker build -t myapp:v1 -f Dockerfile.prod .  # Custom Dockerfile
docker build --no-cache -t myapp:v1 .   # Build without cache
docker build --target builder -t myapp:build .  # Multi-stage target
```

## Build Context

The build context is the set of files sent to the Docker daemon. Control with `.dockerignore`.

## Multi-Stage Builds

```dockerfile
FROM node:18 AS builder
WORKDIR /app
COPY package*.json .
RUN npm ci
COPY . .
RUN npm run build

FROM nginx:alpine
COPY --from=builder /app/dist /usr/share/nginx/html
```

## BuildKit

```bash
DOCKER_BUILDKIT=1 docker build .        # Enable BuildKit
docker build --progress=plain .         # Verbose output
```

## Related Notes

- [[ImageBuilding]] — This note
- [[DockerImage]] — Docker image concepts
- [[Dockerfile]] — Dockerfile reference
- [[OfficialDocs]] — Official documentation
