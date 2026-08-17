---
id: docker-logs
aliases: []
tags: []
---

# docker logs

Fetch the logs of a container.

## Syntax

```bash
docker logs [OPTIONS] CONTAINER
```

## Options

| Option | Purpose |
|---|---|
| `-f` | Follow (tail -f style, stream new output) |
| `--tail N` | Show last N lines |
| `--since` | Show logs since timestamp |
| `-t` | Show timestamps |

## Examples

```bash
# All logs
docker logs <container>

# Follow live output
docker logs -f <container>

# Last 50 lines
docker logs --tail 50 <container>

# Logs with timestamps
docker logs -t <container>

# Logs from last 10 minutes
docker logs --since 10m <container>
```

## Notes

- Logs are stored by the log driver (default: `json-file`).
- Logs persist even after container stops (until container is removed).
- Use `docker logs` for containers that output to stdout/stderr.

## Related Notes

- [[Commands/docker-exec|docker exec]]
- [[DockerContainer]]
- [[DockerDaemon]]
