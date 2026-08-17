---
id: docker-port
aliases: []
tags: []
---

# docker port

List port mappings for a container.

## Syntax

```bash
docker port CONTAINER [PRIVATE_PORT[/PROTOCOL]]
```

## Examples

```bash
# Show all port mappings
docker port mycontainer

# Show mapping for a specific port
docker port mycontainer 80
```

## Output

```
0.0.0.0:8080->80/tcp
0.0.0.0:8443->443/tcp
```

Format: `hostIP:hostPort->containerPort/protocol`

## When to use

- Quickly find which host port maps to which container port.
- Scripting: extract port for curl or other tools.
- Debugging port configuration without running `docker inspect`.

## Notes

- Only shows published ports (ones set with `-p` or `-P`).
- For more detail, use `docker inspect --format '{{.NetworkSettings.Ports}}'`.

## Related Notes

- [[Commands/docker-run|docker run]]
- [[Commands/docker-inspect|docker inspect]]
- [[DockerContainer]]
