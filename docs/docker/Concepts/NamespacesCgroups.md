---
id: NamespacesCgroups
aliases: []
tags: []
---

# Namespaces and cgroups

Docker containers are not virtual machines. They are isolated Linux processes that share the host kernel. Two kernel features make this possible: namespaces and cgroups.

## Namespaces — isolation

Namespaces control what a container can **see**. Each container gets its own isolated view of:

| Namespace | What it isolates |
|---|---|
| PID | Process IDs (container sees its own PID 1) |
| NET | Network interfaces, IP addresses, routing tables |
| MNT | Filesystem mount points |
| UTS | Hostname and domain name |
| IPC | Inter-process communication |
| USER | User and group IDs |

## cgroups — resource limits

cgroups control what a container can **use**. They enforce hard limits on:

- CPU time
- Memory
- Disk I/O
- Network bandwidth

```bash
# Limit a container to 512MB RAM and 0.5 CPU
docker run -d --memory=512m --cpus=0.5 nginx
```

## Why this matters

- Containers start in seconds (no boot process).
- Containers share the host kernel (lightweight).
- Two containers on the same host don't see each other's processes or network.
- A misbehaving container cannot starve the host or other containers (if limits are set).

## Related Notes

- [[WhatIsDocker]]
- [[DockerVsVm]]
- [[DockerContainer]]
