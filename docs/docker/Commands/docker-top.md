---
id: docker-top
aliases: []
tags: []
---

# docker top

Display the running processes inside a container.

## Syntax

```bash
docker top CONTAINER [ps OPTIONS]
```

## Examples

```bash
# Basic process list
docker top mycontainer

# With custom ps flags
docker top mycontainer -aux
docker top mycontainer -o pid,comm,%cpu,%mem
```

## Output

Shows the same columns as `ps` on the host: PID, USER, TIME, COMMAND (and others depending on flags).

## When to use

- Debugging what a container is actually running.
- Checking if a process crashed inside a running container.
- Verifying resource usage at the process level.

## Notes

- Container must be running.
- Processes are visible from the host's PID namespace (not isolated).

## Related Notes

- [[Commands/docker-exec|docker exec]]
- [[Commands/docker-inspect|docker inspect]]
- [[Commands/docker-stats|docker stats]]
