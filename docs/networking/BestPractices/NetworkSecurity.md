---
id: NetworkSecurity
aliases: []
tags: []
---

# Network Security

Best practices for securing network infrastructure.

## Principle of Least Privilege

- Allow only necessary traffic
- Use specific ports, not ranges
- Restrict source IPs when possible
- Default deny, explicit allow

## SSH Hardening

```bash
# /etc/ssh/sshd_config
Port 2222                                    # Change default port
PermitRootLogin no                           # Disable root login
PasswordAuthentication no                    # Key-based only
AllowUsers deploy admin                      # Restrict users
MaxAuthTries 3                               # Limit attempts
```

## Network Segmentation

```
DMZ (192.168.1.0/24)     → Public services
Internal (192.168.2.0/24) → Servers
Management (192.168.3.0/24) → Admin access
```

## Monitoring

```bash
# Log dropped packets
sudo iptables -A INPUT -j LOG --log-prefix "DROPPED: "

# Monitor connections
ss -tunlp                                    # Active connections
netstat -an | grep :22                       # SSH connections
```

## Related Notes

- [[FirewallRules]] - Firewall configuration
- [[DnsSpoofing]] - DNS security
- [[TroubleshootingSecurity]] - Security issues
