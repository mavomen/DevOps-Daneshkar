---
id: CiCdWithDocker
aliases: []
tags: []
---

# CI/CD with Docker

Using Docker in CI/CD pipelines for consistent, reproducible builds.

## Core pattern

```yaml
# GitHub Actions example
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: Build image
        run: docker build -t myapp:${{ github.sha }} .

      - name: Run tests
        run: docker run --rm myapp:${{ github.sha }} npm test

      - name: Push to registry
        run: |
          docker tag myapp:${{ github.sha }} myuser/myapp:${{ github.sha }}
          docker push myuser/myapp:${{ github.sha }}
```

## Layer caching in CI

Without caching, every build starts from scratch. Use `--cache-from`:

```yaml
- name: Build with cache
  run: |
    docker build \
      --cache-from type=registry,ref=myuser/myapp:latest \
      --build-arg BUILDKIT_INLINE_CACHE=1 \
      -t myapp:${{ github.sha }} .
```

Or use BuildKit cache mounts:

```dockerfile
RUN --mount=type=cache,target=/root/.cache/pip \
    pip install -r requirements.txt
```

## Multi-stage in CI

Build in a heavy image, test, then push only the slim final image:

```dockerfile
# Stage 1: Build
FROM node:20 AS builder
WORKDIR /app
COPY . .
RUN npm ci && npm run build

# Stage 2: Test
FROM builder AS test
RUN npm test

# Stage 3: Production
FROM node:20-alpine
COPY --from=builder /app/dist ./dist
CMD ["node", "dist/index.js"]
```

```bash
# Build and test
docker build --target test -t myapp:test .
docker run --rm myapp:test

# Build production only
docker build --target production -t myapp:prod .
```

## Registry auth in pipelines

```bash
# Use credentials from secrets
echo $DOCKER_PASSWORD | docker login -u $DOCKER_USERNAME --password-stdin

# Or use a token
docker login -u $TOKEN_USER --password-stdin < registry.example.com
```

## .dockerignore impact

A good `.dockerignore` speeds up builds and prevents leaks:

```
.git
node_modules
.env
*.md
docker-compose.yml
.github
```

Without it, every build sends the entire directory (including `.git` history) to the daemon.

## Related Notes

- [[DockerfileBestPractices]]
- [[MultiStageBuild]]
- [[BuildKit]]
- [[DockerCompose]]
