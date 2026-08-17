---
id: TroubleshootingConnectivity
aliases: []
tags: []
---

# Troubleshooting Network Connectivity

Diagnose and resolve basic network connectivity issues.

## Diagnostic Flow

```bash
# 1. Check local interface
ip addr show eth0

# 2. Check gateway
ip route show default
ping -c 4 192.168.1.1

# 3. Check DNS
ping -c 4 8.8.8.8
dig google.com

# 4. Check remote host
ping -c 4 target-host
traceroute target-host
```

## Common Issues

| Symptom | Likely Cause | Fix |
|---------|--------------|-----|
| No IP address | DHCP failure | `sudo dhclient eth0` |
| Cannot reach gateway | Cable/switch issue | Check physical connection |
| Can ping IP, not hostname | DNS issue | Check `/etc/resolv.conf` |
| Can ping, no HTTP | Port blocked | Check firewall rules |

## Quick Fixes

```bash
# Renew DHCP
sudo dhclient -r eth0 && sudo dhclient eth0

# Restart networking
sudo systemctl restart networking

# Reset iptables
sudo iptables -F
```

## Related Notes

- [[NetworkInterfaces]] — Interface configuration
- [[TroubleshootingDns]] — DNS issues
- [[FirewallRules]] — Firewall configuration
