---
id: docker-stats
aliases: []
tags: []
---

# docker stats

Display real-time resource usage statistics for running containers.

## Syntax

```bash
docker stats [OPTIONS] [CONTAINER...]
```

## Examples

```bash
# All running containers
docker stats

# Specific container
docker stats mycontainer

# One-shot (no stream)
docker stats --no-stream

# Custom format
docker stats --format "table {{.Name}}\t{{.CPUPerc}}\t{{.MemUsage}}"
```

## Output columns

| Column | Meaning |
|---|---|
| NAME | Container name |
| CPU % | CPU usage percentage |
| MEM USAGE / LIMIT | Memory used / max allowed |
| MEM % | Memory usage percentage |
| NET I/O | Network bytes in/out |
| BLOCK I/O | Disk bytes in/out |
| PIDS | Number of processes |

## When to use

- Real-time monitoring of container performance.
- Identifying containers that consume too much CPU or memory.
- Quick health check without setting up Prometheus/Grafana.

## Notes

- Only works for running containers.
- Equivalent to running `cgroup` stats on the host.
- For historical metrics, use Prometheus with cAdvisor or Docker metrics endpoint.

## Related Notes

- [[Commands/docker-top|docker top]]
- [[Commands/docker-inspect|docker inspect]]
- [[DockerContainer]]
