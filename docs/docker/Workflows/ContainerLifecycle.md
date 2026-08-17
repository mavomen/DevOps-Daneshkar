---
id: ContainerLifecycle
aliases: []
tags: []
---

# Container Lifecycle

The full lifecycle of a Docker container from creation to removal.

## States

```
Created → Running → Paused → Stopped → Removed
```

| State | Transition |
|---|---|
| Created | `docker create` or `docker run` (before start) |
| Running | `docker start` or `docker run` |
| Paused | `docker pause` (freezes processes with SIGSTOP) |
| Stopped | `docker stop` (SIGTERM then SIGKILL) or process exits |
| Removed | `docker rm` |

## Common lifecycle patterns

### Quick one-off run

```bash
docker run --rm ubuntu echo "hello"
# Container is created, runs, and removed automatically
```

### Interactive debugging

```bash
docker run -dit --name debug ubuntu
docker exec -it debug bash
# ... investigate ...
docker stop debug && docker rm debug
```

### Production container

```bash
docker run -dit \
  --name web \
  --restart=unless-stopped \
  -p 80:80 \
  -v web-data:/usr/share/nginx/html \
  nginx
```

### Full commit workflow

```bash
docker run -dit --name build ubuntu
docker exec -it build bash   # make changes
docker commit build myapp:v1 # save state as image
docker rm build               # clean up container
```

## Related Notes

- [[DockerContainer]]
- [[Commands/docker-run|docker run]]
- [[Commands/docker-exec|docker exec]]
- [[Commands/docker-rm|docker rm]]
- [[Commands/docker-commit|docker commit]]
