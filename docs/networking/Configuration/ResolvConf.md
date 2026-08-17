---
id: ResolvConf
aliases: []
tags: []
---

# /etc/resolv.conf

DNS resolver configuration file for Linux systems.

## Syntax

```
nameserver 8.8.8.8
nameserver 8.8.4.4
search example.com
domain example.com
options timeout:2 attempts:3
```

## Fields

| Field | Purpose | Example |
|-------|---------|---------|
| `nameserver` | DNS server IP | `nameserver 8.8.8.8` |
| `search` | Domains to append | `search example.com` |
| `domain` | Default domain | `domain example.com` |
| `options` | Resolver options | `options timeout:2` |

## Common DNS Servers

| Provider | Primary | Secondary |
|----------|---------|-----------|
| Google | `8.8.8.8` | `8.8.4.4` |
| Cloudflare | `1.1.1.1` | `1.0.0.1` |
| Quad9 | `9.9.9.9` | `149.112.112.112` |

## Related Notes

- [[DnsResolution]] - DNS resolution process
- [[TroubleshootingDns]] - DNS troubleshooting
- [[NetworkConfiguration]] - Network setup overview
