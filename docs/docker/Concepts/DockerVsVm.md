---
id: DockerVsVm
aliases: []
tags: []
---

# Docker vs Virtual Machines

Both provide isolation, but at fundamentally different levels. Containers share the host OS kernel; VMs include a full guest OS.

## Comparison

| Feature | Containers | Virtual Machines |
|---|---|---|
| OS | Share host kernel | Each VM has its own OS |
| Size | MBs | GBs |
| Startup | Seconds | Minutes |
| Performance | Near-native | Overhead from hypervisor |
| Isolation | Process-level (namespaces) | Hardware-level (hypervisor) |
| Density | Hundreds per host | Tens per host |

## Architecture

```
VM:        Hardware → Hypervisor → Guest OS → App
Container: Hardware → Host OS → Container Engine → App
```

## When to use what

| Use case | Choice |
|---|---|
| Microservices | Containers |
| CI/CD pipelines | Containers |
| Running different OS kernels | VMs |
| Legacy apps needing full OS | VMs |
| Strong security isolation | VMs |

## Related Notes

- [[WhatIsDocker]]
- [[NamespacesCgroups]]
