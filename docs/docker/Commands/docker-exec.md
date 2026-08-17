---
id: docker-exec
aliases: []
tags: []
---

# docker exec

Run a command inside a running container.

## Syntax

```bash
docker exec [OPTIONS] CONTAINER COMMAND
```

## Common usage

```bash
# Open an interactive bash shell
docker exec -it <container> /bin/bash

# Run a single command
docker exec <container> ls /var/log

# Run as specific user
docker exec -u root <container> apt update

# Set environment variable for the command
docker exec -e MY_VAR=hello <container> env
```

## exec vs run

| `docker exec` | `docker run` |
|---|---|
| Runs in an existing container | Creates a new container |
| Used for debugging / inspection | Used to start a new workload |

## Tips

- Container must be **running** (not stopped).
- Use `-it` for interactive sessions, omit for one-off commands.
- If `bash` is not available, try `sh`.

## Related Notes

- [[Commands/docker-run|docker run]]
- [[DockerContainer]]
- [[Commands/docker-logs|docker logs]]
