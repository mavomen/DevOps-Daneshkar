---
id: DockerNetworking
aliases: []
tags: []
---

# Docker Networking

Docker networking enables containers to communicate with each other, the host, and the outside world.

## Network drivers

| Driver | Scope | Description |
|---|---|---|
| bridge | Single host | Default. Containers on same bridge communicate via internal DNS. |
| host | Single host | Container shares host network stack. No isolation. |
| none | Single host | No networking at all. |
| overlay | Multi-host | Container-to-container across hosts (Swarm). |
| macvlan | Single host | Container gets its own MAC address on the physical network. |

## Bridge networking (default)

When you `docker run`, the container joins the default `bridge` network.

```bash
# Default bridge — containers can't resolve each other by name
docker run -d --name web nginx
docker run -d --name app alpine ping web  # FAILS

# Custom bridge — DNS resolution works
docker network create mynet
docker run -d --name web --network mynet nginx
docker run -d --name app --network mynet alpine ping web  # WORKS
```

## DNS resolution

On custom networks, Docker embeds a DNS server that resolves container names to IPs.

```bash
# From inside app container:
ping web         # resolves to web's IP
curl http://web  # works across containers
```

On the default bridge, only `--link` (legacy) or IPs work.

## Port publishing

Expose container ports to the host:

```bash
# Map host port 8080 to container port 80
docker run -p 8080:80 nginx

# Map to specific host IP
docker run -p 127.0.0.1:8080:80 nginx

# Map UDP
docker run -p 53:53/udp dns-server

# Random host port
docker run -P nginx  # uses EXPOSE directives
```

Format: `hostIP:hostPort:containerPort/protocol`

## Connect/inspect

```bash
# Attach a running container to a network
docker network connect mynet mycontainer

# Detach
docker network disconnect mynet mycontainer

# Inspect network details
docker network inspect mynet
```

## Network isolation patterns

| Pattern | How |
|---|---|
| Frontend/backend separation | Two networks, each service on one |
| Public-only | `--network host` or publish ports |
| Fully isolated | `--network none` |

```bash
# Frontend/backend isolation
docker network create frontend
docker network create backend

docker run -d --name web --network frontend nginx
docker run -d --name api --network frontend --network backend myapp
docker run -d --name db --network backend postgres

# web can reach api, api can reach db, web cannot reach db
```

## Related Notes

- [[DockerDaemon]]
- [[Commands/docker-network|docker network]]
- [[Commands/docker-run|docker run]]
- [[DockerCompose]]
