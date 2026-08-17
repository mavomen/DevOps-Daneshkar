---
id: RootlessDocker
aliases: []
tags: []
---

# Rootless Docker

Rootless Docker runs the Docker daemon and containers as a non-root user, improving security by eliminating root privileges.

## Why rootless

- The default Docker daemon runs as root. If a container escapes, it has root on the host.
- Rootless mode runs everything under your user account.
- Uses user namespaces to remap container root to an unprivileged host user.

## Install rootless Docker

```bash
# Prerequisites
sudo apt install uidmap dbus-user-session

# Install
dockerd-rootless-setuptool.sh install

# Set environment
export PATH=/usr/bin:$PATH
export DOCKER_HOST=unix:///run/user/$(id -u)/docker.sock
```

## How it works

| Component | Root mode | Rootless mode |
|---|---|---|
| daemon | Runs as root | Runs as your user |
| Container root | Maps to host root | Maps to unprivileged UID |
| Port binding | Any port (<1024 OK) | Only ports >1024 |
| Storage | `/var/lib/docker` | `~/.local/share/docker` |

## Limitations

- Cannot bind to ports below 1024 (use `sysctl` or `setcap` to allow).
- No `--network host` (uses slirp4netns instead).
- No AppArmor or seccomp profiles by default.
- Some storage drivers may not work (overlay2 needs kernel 5.11+).

## Verify

```bash
docker info | grep -i root
# Should show: Security Options: rootless
```

## When to use

- Development machines (single user).
- CI/CD runners where you want to limit blast radius.
- Any environment where running as root is a policy violation.

## Related Notes

- [[SecurityBestPractices]]
- [[DockerDaemon]]
- [[WhatIsDocker]]
