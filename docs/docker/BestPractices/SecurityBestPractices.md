---
id: SecurityBestPractices
aliases: []
tags: []
---

# Security Best Practices

Docker containers run as root by default. Follow these practices to reduce attack surface.

## 1. Don't run as root

```dockerfile
RUN addgroup -S appgroup && adduser -S appuser -G appgroup
USER appuser
```

## 2. Don't store secrets in images

```dockerfile
# Bad — baked into the image layer
ENV DB_PASSWORD=secret123

# Better — pass at runtime
# docker run -e DB_PASSWORD=secret123 myapp

# Best — use Docker secrets or a vault
```

## 3. Scan images for vulnerabilities

```bash
docker scout cves myimage:v1    # Docker Scout
trivy image myimage:v1          # Trivy (open source)
```

## 4. Use specific image tags

```dockerfile
# Bad — unpredictable
FROM node:latest

# Good — pinned
FROM node:20.11.1-alpine3.19
```

## 5. Use read-only filesystem where possible

```bash
docker run --read-only --tmpfs /tmp myapp
```

## 6. Limit resources

```bash
docker run --memory=512m --cpus=1.0 myapp
```

## 7. Don't mount Docker socket

```bash
# Dangerous — gives container full Docker access
docker run -v /var/run/docker.sock:/var/run/docker.sock
```

## 8. Use .dockerignore

Prevent `.env`, `.git`, secrets files, and other sensitive data from entering the build context.

## 9. Drop Linux capabilities

By default, containers get a subset of root capabilities. Drop what you don't need:

```bash
# Drop all, add only what's needed
docker run --cap-drop=ALL --cap-add=NET_BIND_SERVICE myapp
```

## 10. Prevent privilege escalation

```bash
# No new privileges even if the binary is setuid
docker run --security-opt=no-new-privileges:true myapp
```

## 11. Use security profiles

```bash
# AppArmor (Ubuntu/Debian)
docker run --security-opt apparmor=docker-default myapp

# Seccomp (syscall filtering)
docker run --security-opt seccomp=profile.json myapp
```

## 12. Sign and verify images

```bash
# Sign with cosign
cosign sign --key cosign.key myuser/myapp:v1

# Verify before pulling
cosign verify --key cosign.pub myuser/myapp:v1
```

## Related Notes

- [[DockerfileBestPractices]]
- [[Dockerfile]]
- [[RootlessDocker]]
- [[BuildKit]]
