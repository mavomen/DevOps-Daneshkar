---
id: docker-run
aliases: []
tags: []
---

# docker run

Create and start a container from an image. This is the most frequently used Docker command.

## Syntax

```bash
docker run [OPTIONS] IMAGE [COMMAND]
```

## Common options

| Option | Purpose |
|---|---|
| `-d` | Detached (background) |
| `-it` | Interactive + TTY (terminal) |
| `-dit` | Detached + interactive + TTY |
| `--name` | Assign a name to the container |
| `-p host:container` | Map host port to container port |
| `-e VAR=value` | Set environment variable |
| `-v volume:/path` | Mount a volume |
| `--network` | Connect to a network |
| `--dns` | Set DNS server |
| `--hostname` | Set container hostname |
| `--restart` | Restart policy (`always`, `unless-stopped`, `no`) |

## Examples

```bash
# Interactive — attaches terminal, stops when you exit
docker run -it ubuntu bash

# Detached — runs in background
docker run -dit ubuntu

# Named container with port mapping
docker run -dit --name web -p 8080:80 nginx

# Multiple port mappings
docker run -dit --name web -p 80:80 -p 443:443 nginx

# Bind to specific IP
docker run -dit --name web -p 127.0.0.1:8080:80 nginx

# With environment variable
docker run -dit -e APP_ENV=production myapp

# With DNS and restart policy
docker run -dit --dns 8.8.8.8 --hostname myhost --restart=always nginx
```

## What happens under the hood

`docker run` = `docker pull` (if not local) + `docker create` + `docker start`

## Related Notes

- [[DockerContainer]]
- [[Commands/docker-ps|docker ps]]
- [[Commands/docker-exec|docker exec]]
- [[Commands/docker-rm|docker rm]]
