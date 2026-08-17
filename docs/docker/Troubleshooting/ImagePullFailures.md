---
id: ImagePullFailures
aliases: []
tags: []
---

# Image Pull Failures

Common errors when pulling images from a registry.

## "unauthorized: authentication required"

```bash
docker pull myuser/myapp:v1
# Error: unauthorized: authentication required

# Fix: log in first
docker login
# Enter credentials when prompted
```

## "toomanyrequests: You have reached your pull rate limit"

```bash
# Docker Hub anonymous: 100 pulls / 6 hours
# Error: toomanyrequests: You have reached your pull rate limit

# Fix 1: log in with a Docker Hub account (200 pulls / 6 hours)
docker login

# Fix 2: use a mirror registry
# Add to /etc/docker/daemon.json:
# { "registry-mirrors": ["https://mirror.example.com"] }

# Fix 3: wait for the limit to reset
```

## "manifest for X not found"

```bash
# Error: manifest for nginx:nonexistent not found
# Cause: tag doesn't exist

# Fix: check available tags
docker hub search nginx
# or
curl -s "https://hub.docker.com/v2/repositories/library/nginx/tags?page_size=10"
```

## "network timeout" or "connection refused"

```bash
# Check DNS
cat /etc/resolv.conf

# Check connectivity
curl -I https://registry-1.docker.io/v2/

# Check proxy settings
export HTTP_PROXY=http://proxy:8080
export HTTPS_PROXY=http://proxy:8080

# Restart daemon after proxy change
sudo systemctl restart docker
```

## "i/o timeout" on large images

```bash
# Pull with timeout
docker pull --quiet myimage:v1

# Or pull specific platform
docker pull --platform linux/amd64 myimage:v1
```

## Related Notes

- [[Registry]]
- [[DockerDaemon]]
- [[Commands/docker-pull|docker pull]]
