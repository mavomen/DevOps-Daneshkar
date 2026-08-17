---
id: OomKilled
aliases: []
tags: []
---

# OOM Killed

Container killed by the host kernel due to exceeding its memory limit.

## How to identify

```bash
# Check container state
docker inspect <container> --format '{{.State.OOMKilled}}'
# true = killed by OOM

# Check exit code
docker inspect <container> --format '{{.State.ExitCode}}'
# 137 = SIGKILL (usually OOM)

# Check logs for the last output before kill
docker logs --tail 50 <container>
```

## Why it happens

- Container exceeded `--memory` limit.
- Host ran out of physical memory.
- Application has a memory leak.

## Fix: increase memory limit

```bash
# Give the container more memory
docker run -d --memory=1g --memory-swap=1g myapp

# Or in compose
# services:
#   app:
#     deploy:
#       resources:
#         limits:
#           memory: 1G
```

## Fix: diagnose memory usage

```bash
# Real-time memory stats
docker stats <container>

# Detailed memory breakdown
docker inspect <container> --format '{{.HostConfig.Memory}}'
docker inspect <container> --format '{{.HostConfig.MemoryReservation}}'

# Find which process is using the most memory
docker exec <container> ps aux --sort=-%mem | head
```

## Fix: application-level

- Check for memory leaks (heap dumps, profiling).
- Reduce Node.js heap: `NODE_OPTIONS="--max-old-space-size=512"`
- Reduce Java heap: `-Xmx512m`
- Add swap space: `--memory-swap=2g`

## Preventive measures

```bash
# Set memory limits in production
docker run -d \
  --memory=512m \
  --memory-swap=512m \
  --memory-reservation=256m \
  myapp

# Monitor with restart policy
docker run -d --restart=unless-stopped --memory=512m myapp
```

## Related Notes

- [[DockerContainer]]
- [[Commands/docker-stats|docker stats]]
- [[Commands/docker-inspect|docker inspect]]
- [[DockerCompose]]
