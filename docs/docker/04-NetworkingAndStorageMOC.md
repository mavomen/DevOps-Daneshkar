---
id: 04-NetworkingAndStorageMOC
aliases: []
tags: []
---

# Networking & Storage (MOC)

Container networking, volumes, and cleanup.

## Networking

- [[DockerNetworking|Docker Networking]]
- [[Commands/docker-network|docker network]]
- [[DockerDaemon|Docker Daemon (daemon.json DNS)]]

```bash
docker network create mynet
docker run -d --name web --network mynet nginx
docker run -d --name app --network mynet ubuntu
# app can reach web at: http://web:80
```

## Storage

- [[Commands/docker-volume|docker volume]]

```bash
docker volume create mydata
docker run -d -v mydata:/app/data nginx
```

## Cleanup

- [[Commands/docker-prune|docker prune]]
- [[Commands/docker-volume|docker volume prune]]

## Configuration

- [[DockerCompose|Docker Compose]]
- [[ComposeProfiles|Compose Profiles]]
- [[DaemonConfiguration|Daemon Configuration]]

## Troubleshooting

- [[NetworkingIssues|Networking Issues]]
