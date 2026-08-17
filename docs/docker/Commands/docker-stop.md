---
id: docker-stop
aliases: []
tags: []
---

# docker stop / start / kill / pause

Control the state of running containers.

## docker stop — graceful shutdown

Sends SIGTERM, then SIGKILL after a timeout (default 10s).

```bash
docker stop <container>
docker stop -t 30 <container>   # custom timeout in seconds
```

## docker start — restart a stopped container

```bash
docker start <container>
docker start -a <container>    # attach to output
docker start -i <container>    # interactive
```

## docker kill — force stop

Sends SIGKILL immediately (no graceful shutdown).

```bash
docker kill <container>
docker kill --signal=SIGHUP <container>   # custom signal
```

## docker pause / unpause — freeze processes

Uses cgroups freezer to suspend all processes without stopping the container.

```bash
docker pause <container>
docker unpause <container>
```

## stop vs kill vs pause

| Command | Signal | Use case |
|---|---|---|
| `stop` | SIGTERM → SIGKILL | Graceful shutdown (let app clean up) |
| `kill` | SIGKILL | Unresponsive container, force stop |
| `pause` | SIGSTOP (freeze) | Free resources temporarily, resume later |

## Related Notes

- [[DockerContainer]]
- [[Commands/docker-rm|docker rm]]
- [[Commands/docker-ps|docker ps]]
