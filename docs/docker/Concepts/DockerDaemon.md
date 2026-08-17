---
id: DockerDaemon
aliases: []
tags: []
---

# Docker Daemon

Docker uses a client-server architecture. The daemon (`dockerd`) is the background service that manages Docker objects.

## Architecture

```
CLI (docker) → REST API → dockerd (daemon) → containerd → runc → container
```

| Component | Role |
|---|---|
| Docker CLI (`docker`) | Sends commands from the terminal |
| REST API | HTTP interface between CLI and daemon |
| dockerd | Main daemon, manages images, containers, networks |
| containerd | Low-level container runtime |
| runc | Creates and runs individual containers |

## Common setup

Grant a non-root user access to the Docker daemon:

```bash
sudo usermod -aG docker $USER
# Log out and back in for changes to take effect
```

## Daemon configuration

The daemon reads config from `/etc/docker/daemon.json`:

```json
{
  "storage-driver": "overlay2",
  "log-driver": "json-file",
  "log-opts": {
    "max-size": "10m",
    "max-file": "3"
  }
}
```

## Related Notes

- [[WhatIsDocker]]
- [[DockerContainer]]
- [[DockerCompose]]
