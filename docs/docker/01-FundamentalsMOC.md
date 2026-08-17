---
id: 01-FundamentalsMOC
aliases: []
tags: []
---

# Fundamentals (MOC)

What Docker is, how it works under the hood, and how it compares to VMs.

## Concepts

- [[WhatIsDocker|What Is Docker]]
- [[DockerImage|Docker Image]]
- [[DockerContainer|Docker Container]]
- [[ImageLayers|Image Layers]]
- [[NamespacesCgroups|Namespaces & cgroups]]
- [[DockerVsVm|Docker vs VM]]
- [[DockerDaemon|Docker Daemon]]
- [[DockerNetworking|Docker Networking]]

## Essential commands

1. Run a container
   - [[Commands/docker-run|docker run]]
2. List containers
   - [[Commands/docker-ps|docker ps]]
3. Enter a container
   - [[Commands/docker-exec|docker exec]]
4. View logs
   - [[Commands/docker-logs|docker logs]]
5. Control state
   - [[Commands/docker-stop|docker stop / start / kill]]
6. Monitor
   - [[Commands/docker-stats|docker stats]]

## Quick start

```bash
docker run -dit --name web -p 8080:80 nginx
docker ps
curl http://localhost:8080
docker exec -it web bash
docker stop web && docker rm web
```

## Quick reference

- [[CommonCommands]] - Frequently used commands
- [[PortMapping]] - Port mapping syntax
- [[ComposeCheatsheet]] - Compose command reference
- [[OfficialDocs]] - Official documentation links
