---
id: 04-SecurityAndDiagnosticsMOC
aliases: []
tags: []
---

# Security & Diagnostics (MOC)

Firewalls, packet capture, port scanning, and network diagnostics.

## Concepts

- [[Firewall|Firewall]]

## Firewall commands

- [[Commands/iptables|iptables]]
- [[Commands/firewalld|firewalld & UFW]]

## Diagnostic commands

- [[Commands/tcpdump|tcpdump]]
- [[Commands/wireshark|wireshark]]
- [[Commands/ping|ping]]
- [[Commands/traceroute|traceroute]]
- [[Commands/nmap|nmap]]

## Quick Commands

```bash
# Capture traffic on port 80
sudo tcpdump port 80

# Check what's listening
ss -tlnp

# Test connectivity
ping -c 4 8.8.8.8

# Trace route
traceroute google.com

# Scan ports on a host
nmap -sV 192.168.1.20
```

## Best Practices

- [[NetworkSecurity]] — Security hardening
- [[NetworkPerformance]] — Performance optimization

## Related Notes

- [[00-Networking|Networking Overview]]
