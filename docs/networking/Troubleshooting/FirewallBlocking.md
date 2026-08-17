---
id: FirewallBlocking
aliases: []
tags: []
---

# Firewall Blocking

Diagnosing when a firewall is preventing traffic.

## Diagnose

```bash
# Check iptables rules
sudo iptables -L -n -v

# Check UFW status
sudo ufw status verbose

# Check firewalld
sudo firewall-cmd --list-all

# Check if a specific port is open
ss -tlnp | grep :80

# Test from another machine
nc -zv 192.168.1.20 80
```

## Common scenarios

| Symptom | Check |
|---|---|
| Can't SSH into server | `sudo iptables -L INPUT -n` — is port 22 allowed? |
| Web app unreachable from outside | `ufw status` — is 80/443 open? |
| Docker container port not accessible | Host firewall vs Docker's own rules |
| Connection times out | `iptables -P INPUT DROP` might be set |

## Quick fixes

```bash
# UFW: allow a port
sudo ufw allow 80/tcp

# iptables: allow a port temporarily
sudo iptables -A INPUT -p tcp --dport 80 -j ACCEPT

# Check Docker's iptables rules
sudo iptables -L DOCKER -n
```

## Docker + firewall interaction

Docker adds its own iptables rules. If the host firewall is blocking traffic, Docker containers may not be reachable even with `-p` port mapping.

```bash
# Check if Docker's rules are present
sudo iptables -L DOCKER -n -v

# If blocked, allow Docker's bridge
sudo iptables -I INPUT -i docker0 -j ACCEPT
```

## Related Notes

- [[Firewall]]
- [[Commands/iptables|iptables]]
- [[Commands/firewalld|firewalld]]
- [[ConnectivityIssues]]
- [[docker/Concepts/DockerNetworking|Docker Networking]]
- [[docker/Commands/docker-network|docker network]]
