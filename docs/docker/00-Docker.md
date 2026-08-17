---
id: 00-Docker
aliases: []
tags: []
---

# Docker Overview (MOC)

This is the entry point for the Docker vault (concepts → commands → workflows → configuration → best practices → troubleshooting).

## Start Here

1. [[01-FundamentalsMOC|01 Fundamentals (MOC)]]
2. [[02-ContainerLifecycleMOC|02 Container Lifecycle (MOC)]]
3. [[03-ImagesAndDockerfilesMOC|03 Images & Dockerfiles (MOC)]]
4. [[04-NetworkingAndStorageMOC|04 Networking & Storage (MOC)]]
5. [[05-BestPracticesMOC|05 Best Practices (MOC)]]
6. [[06-TroubleshootingMOC|06 Troubleshooting (MOC)]]

## Concepts

- [[WhatIsDocker|What Is Docker]]
- [[DockerImage|Docker Image]]
- [[DockerContainer|Docker Container]]
- [[Dockerfile|Dockerfile]]
- [[ImageLayers|Image Layers]]
- [[NamespacesCgroups|Namespaces & cgroups]]
- [[DockerVsVm|Docker vs VM]]
- [[Registry|Registry]]
- [[DockerDaemon|Docker Daemon]]
- [[DockerNetworking|Docker Networking]]
- [[BuildKit|BuildKit]]
- [[RootlessDocker|Rootless Docker]]

## Commands

### Container Operations

- [[Commands/docker-run|docker run]]
- [[Commands/docker-ps|docker ps]]
- [[Commands/docker-exec|docker exec]]
- [[Commands/docker-logs|docker logs]]
- [[Commands/docker-inspect|docker inspect]]
- [[Commands/docker-rm|docker rm]]
- [[Commands/docker-cp|docker cp]]
- [[Commands/docker-stop|docker stop / start / kill / pause]]
- [[Commands/docker-top|docker top]]
- [[Commands/docker-stats|docker stats]]
- [[Commands/docker-port|docker port]]
- [[Commands/docker-diff|docker diff]]
- [[Commands/docker-wait|docker wait]]

### Image Operations

- [[Commands/docker-build|docker build]]
- [[Commands/docker-pull|docker pull]]
- [[Commands/docker-push|docker push]]
- [[Commands/docker-images|docker images]]
- [[Commands/docker-commit|docker commit]]
- [[Commands/docker-tag|docker tag]]
- [[Commands/docker-history|docker history]]
- [[Commands/docker-save|docker save / export]]

### Networking & Storage

- [[Commands/docker-network|docker network]]
- [[Commands/docker-volume|docker volume]]
- [[Commands/docker-prune|docker prune]]

## Configuration

- [[DockerCompose|Docker Compose]]
- [[ComposeProfiles|Compose Profiles]]
- [[DaemonConfiguration|Daemon Configuration]]

## Workflows

- [[MultiStageBuild|Multi-Stage Build]]
- [[ContainerLifecycle|Container Lifecycle]]
- [[CiCdWithDocker|CI/CD with Docker]]
- [[LocalDevEnvironment|Local Dev Environment]]

## Best Practices

- [[DockerfileBestPractices|Dockerfile Best Practices]]
- [[SecurityBestPractices|Security Best Practices]]

## Troubleshooting

- [[ContainerNotFound|Container Not Found]]
- [[NetworkingIssues|Networking Issues]]
- [[PermissionDenied|Permission Denied]]
- [[ImagePullFailures|Image Pull Failures]]
- [[OomKilled|OOM Killed]]

## Note Format

- [[NOTE_FORMAT|Note Format Guide]]
