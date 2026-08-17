---
id: Dns
aliases: []
tags: []
---

# DNS

Domain Name System translates human-readable hostnames into IP addresses. Uses UDP port 53 (TCP for large responses and zone transfers).

## Resolution flow

```
Browser → Local cache → OS cache → Recursive resolver → Root server → TLD server → Authoritative server
```

1. Client checks local cache
2. Query sent to recursive resolver (usually ISP or 8.8.8.8)
3. Resolver queries root servers → finds TLD server (.com, .org)
4. TLD server points to authoritative nameserver
5. Authoritative server returns the IP

## Record types

| Record | Purpose | Example |
|---|---|---|
| A | Hostname → IPv4 | `example.com → 93.184.216.34` |
| AAAA | Hostname → IPv6 | `example.com → 2606:2800:220:1::248` |
| CNAME | Alias to another name | `www.example.com → example.com` |
| MX | Mail server | `example.com → mail.example.com` |
| NS | Nameserver for domain | `example.com → ns1.example.com` |
| TXT | Text data (SPF, DKIM) | `v=spf1 include:_spf.google.com ~all` |
| PTR | Reverse DNS (IP → name) | `34.216.184.93 → example.com` |
| SOA | Start of authority | Zone metadata |

## Key commands

```bash
nslookup example.com
dig example.com
dig +short example.com
dig @8.8.8.8 example.com MX
```

## Related Notes

- [[Commands/nslookup|nslookup]]
- [[Commands/dig|dig]]
- [[Commands/ping|ping]]
- [[TcpAndUdp]]
