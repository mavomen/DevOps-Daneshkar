---
id: 05-BestPracticesMOC
aliases: []
tags: []
---

# Best Practices (MOC)

Writing secure, efficient, and maintainable Dockerfiles and containers.

## Dockerfile practices

- [[DockerfileBestPractices|Dockerfile Best Practices]]
- [[MultiStageBuild|Multi-Stage Build]]
- [[BuildKit|BuildKit]]

## Security

- [[SecurityBestPractices|Security Best Practices]]
- [[RootlessDocker|Rootless Docker]]

## Key rules

- Don't run as root
- Use minimal base images (alpine, slim)
- Pin image versions
- Don't bake secrets into images
- Use `.dockerignore`
- Order Dockerfile instructions by cacheability
- Scan images for vulnerabilities
- Drop Linux capabilities
- Prevent privilege escalation

## Related Notes

- [[Dockerfile|Dockerfile Reference]]
