---
id: TroubleshootingDns
aliases: []
tags: []
---

# Troubleshooting DNS

Diagnose and resolve DNS resolution issues.

## Symptoms → Causes

| Symptom | Likely Cause |
|---------|--------------|
| `Name or service not known` | DNS server unreachable or misconfigured |
| Slow DNS resolution | DNS server overload, network latency |
| Intermittent failures | DNS server redundancy issues |
| Wrong IP returned | DNS cache poisoning, stale records |

## Diagnostic Commands

```bash
dig example.com                            # Full DNS query
dig +short example.com                     # Quick IP lookup
nslookup example.com                       # Basic DNS test
host example.com                           # Simple DNS lookup
cat /etc/resolv.conf                        # Check DNS config
systemd-resolve --status                   # systemd-resolved status
```

## Common Fixes

```bash
# Test with different DNS server
dig @8.8.8.8 example.com

# Flush DNS cache
sudo systemd-resolve --flush-caches

# Fix resolv.conf
echo "nameserver 8.8.8.8" | sudo tee /etc/resolv.conf
```

## Related Notes

- [[DnsResolution]] — DNS resolution process
- [[ResolvConf]] — DNS config file
- [[DnsSpoofing]] — DNS security
