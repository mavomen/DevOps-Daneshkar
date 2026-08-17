---
id: Firewall
aliases: []
tags: []
---

# Firewall

A network security system that monitors and controls traffic based on predefined rules.

## Types

| Type | Description |
|---|---|
| Stateless | Filters packets individually, no context |
| Stateful | Tracks connection state (SYN, ESTABLISHED, etc.) |
| Application (L7) | Inspects payload (e.g., WAF, proxy) |

## Linux firewall stack

```
Application
    ↓
iptables / nftables / firewalld   ← Userspace tools
    ↓
Netfilter                          ← Kernel framework
    ↓
Network packets
```

## Common tools

| Tool | Description |
|---|---|
| iptables | Classic Linux firewall (Netfilter) |
| nftables | Modern replacement for iptables |
| firewalld | Dynamic firewall daemon (CentOS/RHEL) |
| ufw | Uncomplicated Firewall (Ubuntu) |

## Basic iptables

```bash
# Allow SSH
sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT

# Block a specific IP
sudo iptables -A INPUT -s 10.0.0.50 -j DROP

# Allow established connections
sudo iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT

# Default deny incoming
sudo iptables -P INPUT DROP

# Flush all rules
sudo iptables -F
```

## UFW (Ubuntu)

```bash
sudo ufw allow 22/tcp
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp
sudo ufw enable
sudo ufw status verbose
```

## Related Notes

- [[Commands/iptables|iptables]]
- [[Commands/firewalld|firewalld]]
- [[NatAndPAT]]
- [[OsiModel]]
