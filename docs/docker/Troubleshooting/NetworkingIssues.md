---
id: NetworkingIssues
aliases: []
tags: []
---

# Networking Issues

Common networking problems and how to fix them.

## Container can't reach the internet

```bash
# Check DNS resolution inside the container
docker exec <container> cat /etc/resolv.conf
docker exec <container> nslookup google.com

# Try custom DNS
docker run --dns 8.8.8.8 myapp

# Check if IP forwarding is enabled
sysctl net.ipv4.ip_forward
# If 0, enable it:
sudo sysctl -w net.ipv4.ip_forward=1
```

## Container-to-container: name not resolving

```bash
# Problem: ping web fails
docker run --name app alpine ping web

# Fix: use a custom network (not default bridge)
docker network create mynet
docker run -d --name web --network mynet nginx
docker run -d --name app --network mynet alpine
docker exec app ping web  # works
```

## Port not accessible from host

```bash
# Check port mappings
docker port <container>

# Verify the container is listening
docker exec <container> ss -ntlp

# Check if host port is already in use
ss -ntlp | grep :8080

# Check firewall
sudo iptables -L -n | grep 8080
```

## DNS resolution slow or failing

```bash
# Check daemon DNS config
cat /etc/docker/daemon.json
# Add: { "dns": ["8.8.8.8", "8.8.4.4"] }

# Restart daemon
sudo systemctl restart docker
```

## Container can't reach host

```bash
# Linux: use host.docker.internal
docker run --add-host=host.docker.internal:host-gateway myapp

# Or use host network
docker run --network host myapp
```

## Related Notes

- [[DockerNetworking]]
- [[Commands/docker-network|docker network]]
- [[DockerDaemon]]
