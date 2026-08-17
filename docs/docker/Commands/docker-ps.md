---
id: docker-ps
aliases: []
tags: []
---

# docker ps

List containers.

## Syntax

```bash
docker ps [OPTIONS]
```

## Options

| Option | Purpose |
|---|---|
| `-a` | Show all containers (including stopped) |
| `-q` | Quiet output (only IDs) |
| `-s` | Display total file sizes |
| `--filter` | Filter output |
| `--format` | Format output with Go templates |

## Examples

```bash
# Running containers only
docker ps

# All containers
docker ps -a

# All container IDs
docker ps -aq

# Filter by name
docker ps --filter "name=web"

# Filter by status
docker ps -a --filter "status=exited"
```

## Output columns

| Column | Meaning |
|---|---|
| CONTAINER ID | Short SHA of the container |
| IMAGE | Image used to create it |
| COMMAND | Command running inside |
| CREATED | Time since creation |
| STATUS | Up / Exited / Restarting |
| PORTS | Port mappings |
| NAMES | Container name |

## Related Notes

- [[Commands/docker-run|docker run]]
- [[Commands/docker-rm|docker rm]]
- [[DockerContainer]]
