---
id: docker-push
aliases: []
tags: []
---

# docker push

Upload a local image to a container registry (Docker Hub by default).

## Syntax

```bash
docker push [OPTIONS] NAME[:TAG]
```

## Workflow

```bash
# 1. Build your image
docker build -t myapp:v1 .

# 2. Tag for the registry
docker tag myapp:v1 myuser/myapp:v1

# 3. Authenticate
docker login

# 4. Push
docker push myuser/myapp:v1
```

## Push to a private registry

```bash
docker tag myapp:v1 registry.example.com/myapp:v1
docker login registry.example.com
docker push registry.example.com/myapp:v1
```

## Push multiple tags

```bash
docker push myuser/myapp --all-tags
```

## Rate limits

Docker Hub enforces pull rate limits:
- Anonymous: 100 pulls / 6 hours
- Free tier: 200 pulls / 6 hours
- Pro/Team: unlimited

Push is not rate-limited.

## Related Notes

- [[Commands/docker-tag|docker tag]]
- [[Registry]]
- [[Commands/docker-pull|docker pull]]
