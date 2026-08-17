---
id: docker-network
aliases: []
tags: []
---

# docker network

Create and manage networks for container-to-container communication.

## Default networks

```bash
docker network ls
```

| Network | Driver | Description |
|---|---|---|
| bridge | bridge | Default. Containers on same bridge can communicate. |
| host | host | Container shares host's network stack. |
| none | null | No networking. |

## Create a custom network

```bash
docker network create mynetwork
```

## Connect containers to a network

```bash
# Run containers on the same network
docker run -d --name web --network mynetwork nginx
docker run -d --name app --network mynetwork ubuntu

# web and app can now reach each other by name
# e.g., from app: curl http://web:80
```

## Manage networks

```bash
# Connect a running container to a network
docker network connect mynetwork mycontainer

# Disconnect
docker network disconnect mynetwork mycontainer

# Inspect
docker network inspect mynetwork

# Remove
docker network rm mynetwork

# Remove all unused networks
docker network prune
```

## Network drivers

| Driver | Use case |
|---|---|
| bridge | Default, single-host communication |
| host | Best performance, no isolation |
| overlay | Multi-host (Swarm) |
| macvlan | Assign MAC address to container |

## Related Notes

- [[DockerContainer]]
- [[DockerDaemon]]
- [[Commands/docker-run|docker run]]
