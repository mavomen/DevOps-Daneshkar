---
id: docker-wait
aliases: []
tags: []
---

# docker wait

Block until a container stops, then print its exit code.

## Syntax

```bash
docker wait CONTAINER [CONTAINER...]
```

## Examples

```bash
# Wait for a single container
docker wait mycontainer

# Wait for multiple containers
docker wait web app db

# Use in scripts
exit_code=$(docker wait mycontainer)
if [ "$exit_code" -ne 0 ]; then
  echo "Container failed with exit code $exit_code"
fi
```

## When to use

- CI/CD pipelines: wait for a build/test container to finish.
- Scripting: capture exit codes without polling.
- Orchestration: run a one-off task and get its result.

## Notes

- Container must be running (or already stopped).
- Returns the exit code of the container's main process.
- Does not show output — combine with `docker logs` if needed.

## Related Notes

- [[Commands/docker-logs|docker logs]]
- [[Commands/docker-ps|docker ps]]
- [[DockerContainer]]
