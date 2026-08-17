---
id: DockerContainer
aliases: []
tags: []
---

# Docker Container

A container is a running instance of a Docker image. It is an isolated process on the host system with its own filesystem, networking, and process space.

## Lifecycle

```
Created → Running → Paused → Stopped → Removed
```

| State | Command to reach |
|---|---|
| Created | `docker create` |
| Running | `docker start` or `docker run` |
| Paused | `docker pause` |
| Stopped | `docker stop` or Ctrl+C |
| Removed | `docker rm` |

## Running a container

```bash
# Interactive (attaches terminal, stops when you exit)
docker run -it ubuntu bash

# Detached (runs in background)
docker run -dit --name myapp nginx

# With port mapping
docker run -dit -p 8080:80 --name web nginx

# With volume
docker run -dit -v mydata:/app/data --name app nginx
```

## Key commands

```bash
docker ps              # running containers
docker ps -a           # all containers (including stopped)
docker exec -it <id> bash   # enter a running container
docker logs <id>       # view output
docker stop <id>       # graceful shutdown (SIGTERM)
docker kill <id>       # force stop (SIGKILL)
docker rm <id>         # remove stopped container
docker rm -f <id>      # force remove (even if running)
```

## Data persistence

By default, data inside a container is lost when the container is removed. Use volumes to persist data outside the container's writable layer.

## Related Notes

- [[WhatIsDocker]]
- [[DockerImage]]
- [[Commands/docker-run|docker run]]
- [[Commands/docker-exec|docker exec]]
- [[Commands/docker-ps|docker ps]]
