---
id: Registry
aliases: []
tags: []
---

# Registry

A Docker registry is a storage and distribution system for Docker images. You push images to a registry and pull them from anywhere.

## Docker Hub

The default public registry. Think GitHub for Docker images.

```bash
docker pull nginx              # pulls from Docker Hub
docker push myuser/myapp:v1    # pushes to Docker Hub
docker login                   # authenticate before pushing
docker tag myapp:v1 myuser/myapp:v1   # tag for push
```

## Private registries

| Tool | Description |
|---|---|
| Docker Hub (paid) | Private repos with access control |
| Nexus | Repository manager, supports Docker |
| Harbor | Enterprise-grade, with scanning and RBAC |
| AWS ECR | Amazon's managed container registry |
| GitHub GHCR | GitHub Container Registry |
| GitLab Registry | Built into GitLab CI/CD |

## Flow

```
Developer → docker build → image → docker push → Registry → docker pull → Server
```

## Related Notes

- [[DockerImage]]
- [[DockerDaemon]]
- [[Commands/docker-pull|docker pull]]
- [[Commands/docker-tag|docker tag]]
