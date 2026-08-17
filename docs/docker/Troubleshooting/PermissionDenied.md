---
id: PermissionDenied
aliases: []
tags: []
---

# Permission Denied

Common permission errors with Docker containers and volumes.

## "Permission denied" on volume mount

```bash
# Problem: container user can't write to mounted volume
docker run -v /host/data:/app/data myapp
# Error: EACCES: permission denied, open '/app/data/file.txt'
```

**Causes:**
- Container runs as non-root but host directory is owned by root.
- UID/GID mismatch between host and container.

**Fix:**

```bash
# Match host UID to container user
sudo chown -R 1000:1000 /host/data

# Or run container as root (quick fix, not recommended)
docker run -u root -v /host/data:/app/data myapp

# Or set user in Dockerfile
RUN adduser -u 1000 appuser
USER appuser
```

## "Cannot connect to Docker daemon"

```bash
# Problem: permission denied connecting to socket
docker ps
# Cannot connect to Docker daemon at unix:///var/run/docker.sock

# Fix: add user to docker group
sudo usermod -aG docker $USER
# Log out and back in
```

## "OCI runtime create failed: permission denied"

```bash
# Problem: rootless mode with wrong storage driver
# Fix: ensure overlay2 is supported
docker info | grep "Storage Driver"
```

## Container can't write to tmpfs

```bash
# Problem: tmpfs size too small
docker run --read-only --tmpfs /tmp: size=100m myapp
```

## Related Notes

- [[ContainerNotFound]]
- [[DockerContainer]]
- [[SecurityBestPractices]]
