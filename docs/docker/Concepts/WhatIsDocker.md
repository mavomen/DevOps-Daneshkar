---
id: WhatIsDocker
aliases: []
tags: []
---

# What Is Docker

Docker is a platform that packages an application and everything it needs to run (code, libraries, dependencies, configuration) into a container. It runs consistently across environments — laptop, test server, cloud.

## Analogy

Application = a recipe.
Docker container = a lunchbox with the meal and all utensils.
Wherever you take the lunchbox, you get the same meal regardless of what's available locally.

## Why Docker

- **Consistency** — app behaves the same in dev, test, and production.
- **Portability** — containers run on any system with Docker installed.
- **Isolation** — each application runs in its own environment without interference.
- **Fast startup** — containers start in seconds (share host OS kernel).
- **Efficient resources** — lighter than traditional virtual machines.

## Core components

1. **Dockerfile** — text file with instructions for building an image.
2. **Docker Image** — read-only template created from a Dockerfile. Think blueprint.
3. **Docker Container** — running instance of an image. Multiple containers from one image.

```
Dockerfile  →(build)→  Image  →(run)→  Container
```

## Under the hood

Docker uses two Linux kernel features:
- **Namespaces** — isolate what a container can see (network, processes, filesystem).
- **cgroups** — limit what a container can use (CPU, memory, I/O).

## Related Notes

- [[DockerImage]]
- [[DockerContainer]]
- [[Dockerfile]]
- [[NamespacesCgroups]]
- [[DockerVsVm]]
