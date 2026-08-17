---
id: TroubleshootingSecurity
aliases: []
tags: []
---

# Troubleshooting Network Security

Diagnose and resolve network security issues.

## Common Issues

| Issue | Symptom | Fix |
|-------|---------|-----|
| Blocked port | Connection refused | Check firewall rules |
| SSH locked out | Cannot SSH | Use console access, check iptables |
| Rogue service | Unexpected listening port | `ss -tlnp` to identify |
| Traffic interception | Suspicious latency | Check for ARP spoofing |

## Diagnostic Commands

```bash
ss -tlnp                                    # List listening ports
sudo iptables -L -n -v                      # Check firewall rules
arp -a                                      # Check ARP table
sudo tcpdump -i eth0 -nn                    # Capture traffic
```

## Related Notes

- [[NetworkSecurity]] — Security best practices
- [[FirewallRules]] — Firewall configuration
- [[TroubleshootingConnectivity]] — Connectivity issues
