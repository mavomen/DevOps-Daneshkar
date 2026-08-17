---
id: 05-TroubleshootingMOC
aliases: []
tags: []
---

# Troubleshooting (MOC)

Diagnosing and fixing common network issues.

## Problems

- [[ConnectivityIssues|Connectivity Issues]]
- [[DnsResolution|DNS Resolution Issues]]
- [[FirewallBlocking|Firewall Blocking]]

## Diagnostic flow

```
Local interface → Gateway → Internet IP → DNS name → Specific port
```

## Key commands

```bash
# What's my IP?
ip addr show

# Can I reach the gateway?
ping 192.168.1.1

# Can I reach the internet?
ping 8.8.8.8

# Can I resolve names?
dig example.com

# What's listening?
ss -tlnp

# What's in my firewall?
sudo iptables -L -n -v
sudo ufw status verbose

# What route is taken?
traceroute example.com
```

## Related Notes

- [[ConnectivityIssues]]
- [[DnsResolution]]
- [[FirewallBlocking]]
