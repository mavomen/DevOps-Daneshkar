---
id: DnsSpoofing
aliases: []
tags: []
---

# DNS Spoofing

Attack where an attacker redirects DNS queries to malicious destinations.

## How It Works

1. Attacker intercepts DNS queries (ARP spoofing, rogue DNS server)
2. Returns fake IP addresses for legitimate domains
3. Victim connects to attacker-controlled server

## Detection

```bash
dig example.com                            # Check DNS responses
nslookup example.com 8.8.8.8              # Compare with known DNS
tcpdump -i eth0 port 53                    # Monitor DNS traffic
```

## Prevention

- Use DNS over HTTPS (DoH) or DNS over TLS (DoT)
- Validate DNS responses with DNSSEC
- Use trusted DNS servers (8.8.8.8, 1.1.1.1)
- Monitor for unexpected DNS traffic

## Related Notes

- [[DnsResolution]] — DNS resolution process
- [[NetworkSecurity]] — Security hardening
- [[TroubleshootingDns]] — DNS troubleshooting
