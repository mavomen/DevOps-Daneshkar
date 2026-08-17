---
id: DockerfileBestPractices
aliases: []
tags: []
---

# Dockerfile Best Practices

Rules for writing efficient, maintainable Dockerfiles.

## 1. Use minimal base images

```dockerfile
# Prefer
FROM alpine:3.19
FROM node:20-alpine
FROM python:3.12-slim

# Avoid
FROM ubuntu:24.04   # unless you need a full distro
```

## 2. Order instructions by cacheability

Put rarely-changing instructions first, frequently-changing last.

```dockerfile
FROM node:20-alpine

WORKDIR /app

# Rarely changes → cached
COPY package*.json ./
RUN npm ci

# Changes often → rebuilt
COPY . .
RUN npm run build
```

## 3. Use .dockerignore

Exclude files that are not needed in the image:

```
node_modules
.git
.env
*.md
Dockerfile
docker-compose.yml
```

## 4. Combine RUN commands

```dockerfile
# Bad: multiple layers
RUN apt update
RUN apt install -y curl
RUN apt install -y git

# Good: single layer
RUN apt update && apt install -y curl git && rm -rf /var/lib/apt/lists/*
```

## 5. Don't run as root

```dockerfile
RUN addgroup -S appgroup && adduser -S appuser -G appgroup
USER appuser
```

## 6. Use COPY over ADD

`COPY` does exactly what it says. `ADD` has extra features (auto-extracting tarballs, fetching URLs) that are rarely needed and can be surprising.

## 7. Use multi-stage builds

Build in a heavy image, copy artifacts to a slim image. See [[MultiStageBuild]].

## Related Notes

- [[Dockerfile]]
- [[MultiStageBuild]]
- [[SecurityBestPractices]]
