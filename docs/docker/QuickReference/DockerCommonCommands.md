---
id: DockerCommonCommands
aliases: []
tags: []
---

# Docker Common Commands

Quick reference for frequently used Docker commands.

## Container Lifecycle

```bash
docker run -d --name myapp -p 8080:80 nginx    # Run detached
docker start myapp                              # Start stopped container
docker stop myapp                               # Stop running container
docker restart myapp                            # Restart container
docker rm myapp                                 # Remove stopped container
docker rm -f myapp                              # Force remove running container
docker ps                                       # List running containers
docker ps -a                                    # List all containers
```

## Image Management

```bash
docker images                                   # List images
docker pull nginx:latest                        # Pull image
docker build -t myapp:v1 .                      # Build image
docker tag myapp:v1 registry/myapp:v1           # Tag image
docker push registry/myapp:v1                   # Push image
docker rmi myapp:v1                             # Remove image
docker image prune                              # Remove unused images
```

## Debugging

```bash
docker logs myapp                               # View logs
docker logs -f myapp                            # Follow logs
docker exec -it myapp bash                      # Shell into container
docker inspect myapp                            # Container details
docker stats                                    # Resource usage
docker top myapp                                # Running processes
```

## Cleanup

```bash
docker system prune                             # Remove unused data
docker system prune -a                          # Remove all unused data
docker volume prune                             # Remove unused volumes
docker network prune                            # Remove unused networks
```

## Related Notes

- [[DockerCommonCommands]] - Full command reference
- [[ContainerLifecycle]] - Container states and transitions
- [[DockerNetworking]] - Network management commands
