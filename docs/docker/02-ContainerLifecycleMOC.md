---
id: 02-ContainerLifecycleMOC
aliases: []
tags: []
---

# Container Lifecycle (MOC)

Day-to-day container operations: run, inspect, manage, and clean up.

## Create and run

- [[Commands/docker-run|docker run]]
- [[Commands/docker-ps|docker ps]]

## Inspect

- [[Commands/docker-exec|docker exec]]
- [[Commands/docker-logs|docker logs]]
- [[Commands/docker-inspect|docker inspect]]
- [[Commands/docker-cp|docker cp]]
- [[Commands/docker-diff|docker diff]]
- [[Commands/docker-port|docker port]]

## Monitor

- [[Commands/docker-stats|docker stats]]
- [[Commands/docker-top|docker top]]

## Control state

- [[Commands/docker-stop|docker stop / start / kill / pause]]

## Stop and remove

- [[Commands/docker-rm|docker rm]]
- [[Commands/docker-prune|docker prune]]

## Lifecycle workflow

- [[ContainerLifecycle|Container Lifecycle]]

## Tips

```bash
# Quick cleanup of everything
docker rm -f $(docker ps -aq)

# Follow logs of a running container
docker logs -f <container>

# Copy a config file into a running container
docker cp ./nginx.conf web:/etc/nginx/nginx.conf

# Check what changed inside a container
docker diff <container>
```
