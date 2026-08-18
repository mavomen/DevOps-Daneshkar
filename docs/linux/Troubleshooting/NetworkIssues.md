---
id: NetworkIssues
aliases: []
tags: []
---

# Network Issues — Troubleshooting

Diagnosing network connectivity problems.

## Quick Diagnosis

```bash
ip addr show                               # IP addresses
ip route show                              # Routing table
ping -c 4 8.8.8.8                          # External connectivity
ping -c 4 google.com                       # DNS resolution
ss -tlnp                                   # Listening ports
ss -tnp                                    # Established connections
```

## Connectivity Checklist

- [ ] Interface up? `ip link show`
- [ ] IP assigned? `ip addr show`
- [ ] Default route? `ip route show`
- [ ] DNS working? `dig example.com`
- [ ] Firewall? `iptables -L -n`
- [ ] Port listening? `ss -tlnp | grep PORT`

## DNS Issues

```bash
# Test DNS
dig example.com                            # Full query
dig +short example.com                     # Quick answer
nslookup example.com                       # Simple test
cat /etc/resolv.conf                       # DNS servers

# Fix DNS temporarily
echo "nameserver 8.8.8.8" > /etc/resolv.conf

# Flush cache
systemd-resolve --flush-caches
```

## Firewall

```bash
# UFW
ufw status verbose
ufw allow 80/tcp

# iptables
iptables -L -n
iptables -L -n -v                          # With counters
```

## Interface Issues

```bash
# Restart interface
sudo ip link set eth0 down && sudo ip link set eth0 up

# Release/renew DHCP
sudo dhclient -r eth0 && sudo dhclient eth0

# Check cable
ip link show eth0                          # state UP = connected
ethtool eth0                               # Link detected: yes
```

## Related Notes

- [[NetworkingBasics]] — Network fundamentals
- [[FirewallRules]] — Firewall configuration
- [[ResolvConf]] — DNS configuration
- [[SshdConfig]] — SSH config
