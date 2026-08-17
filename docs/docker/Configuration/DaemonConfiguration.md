---
id: DaemonConfiguration
aliases: []
tags: []
---

# Daemon Configuration

The Docker daemon (`dockerd`) can be configured globally via `/etc/docker/daemon.json` or by adding users to the `docker` group.

## Grant docker access to non-root users

```bash
sudo usermod -aG docker $USER
# Log out and back in for group changes to take effect
```

## daemon.json

Located at `/etc/docker/daemon.json`:

```json
{
  "storage-driver": "overlay2",
  "log-driver": "json-file",
  "log-opts": {
    "max-size": "10m",
    "max-file": "3"
  },
  "dns": ["8.8.8.8", "8.8.4.4"],
  "registry-mirrors": ["https://mirror.example.com"]
}
```

## Common settings

| Key | Purpose |
|---|---|
| `storage-driver` | Filesystem driver (`overlay2` is recommended) |
| `log-driver` | Default log driver (`json-file`, `syslog`, `journald`) |
| `log-opts` | Log rotation settings |
| `dns` | Default DNS servers for containers |
| `registry-mirrors` | Mirror registries for faster pulls |
| `insecure-registries` | Registries without TLS (dev only) |
| `data-root` | Docker data directory (default: `/var/lib/docker`) |

## Apply changes

```bash
sudo systemctl daemon-reload
sudo systemctl restart docker
```

## Verify

```bash
docker info          # shows daemon configuration
docker version       # shows client and server versions
```

## Related Notes

- [[DockerDaemon]]
- [[WhatIsDocker]]
