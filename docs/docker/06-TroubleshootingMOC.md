---
id: 06-TroubleshootingMOC
aliases: []
tags: []
---

# Troubleshooting (MOC)

Diagnosing and fixing common Docker issues.

## Common problems

- [[ContainerNotFound|Container Not Found]]
- [[NetworkingIssues|Networking Issues]]
- [[PermissionDenied|Permission Denied]]
- [[ImagePullFailures|Image Pull Failures]]
- [[OomKilled|OOM Killed]]

## Diagnostic commands

```bash
# What's running and what stopped
docker ps -a

# Logs of a specific container
docker logs <container>

# Why did it exit?
docker inspect <container> --format '{{.State.ExitCode}}'
docker inspect <container> --format '{{.State.Error}}'

# OOM killed?
docker inspect <container> --format '{{.State.OOMKilled}}'

# Resource usage
docker stats

# System-wide disk usage
docker system df
```

## Quick fixes

| Problem | Fix |
|---|---|
| Container keeps restarting | `docker logs <container>` to see the error |
| Port already in use | `ss -ntlp` to find the process, stop it or use a different port |
| Permission denied | Check `USER` in Dockerfile or `usermod -aG docker $USER` |
| Out of disk space | `docker system prune --volumes` |
| OOM killed | Increase `--memory` limit or fix memory leak |
| Can't pull image | `docker login` or check rate limits |

## Related Notes

- [[Commands/docker-logs|docker logs]]
- [[Commands/docker-ps|docker ps]]
- [[Commands/docker-inspect|docker inspect]]
