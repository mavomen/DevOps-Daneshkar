---
id: DnsResolution
aliases: []
tags: []
---

# DNS Resolution Issues

Diagnosing and fixing DNS resolution failures.

## Diagnose

```bash
# Test basic resolution
nslookup example.com

# Detailed query
dig example.com

# Check what DNS server is being used
cat /etc/resolv.conf

# Test with a specific DNS server
dig @8.8.8.8 example.com

# Check local hosts file
cat /etc/hosts
```

## Common causes and fixes

| Cause | Fix |
|---|---|
| DNS server unreachable | Change DNS to `8.8.8.8` or `1.1.1.1` |
| Wrong `/etc/resolv.conf` | Edit or regenerate |
| DNS cache stale | `systemd-resolve --flush-caches` |
| Local `/etc/hosts` override | Remove or update the entry |
| Firewall blocking UDP 53 | Open port 53 in firewall |

## Flush DNS cache

```bash
# systemd-resolved
sudo systemd-resolve --flush-caches

# nscd
sudo service nscd restart
```

## Related Notes

- [[Dns]]
- [[Commands/dig|dig]]
- [[Commands/nslookup|nslookup]]
- [[ConnectivityIssues]]
