---
id: dig
aliases: []
tags: []
---

# dig

Domain Information Groper. Detailed DNS lookup tool with precise control over queries.

## Basic usage

```bash
# Resolve hostname
dig example.com

# Short answer only
dig +short example.com

# Query specific DNS server
dig @8.8.8.8 example.com

# Reverse lookup
dig -x 93.184.216.34
```

## Query specific record types

```bash
dig example.com A       # IPv4 address
dig example.com AAAA    # IPv6 address
dig example.com MX      # Mail servers
dig example.com NS      # Nameservers
dig example.com TXT     # Text records
dig example.com CNAME   # Canonical name
dig example.com SOA     # Start of authority
```

## Trace resolution

```bash
# Follow the full resolution path
dig +trace example.com
```

## Useful flags

| Flag | Purpose |
|---|---|
| `+short` | Show only the answer |
| `+noall +answer` | Show only answer section |
| `+trace` | Show full resolution chain |
| `@server` | Query specific DNS server |
| `-x` | Reverse lookup |
| `+tcp` | Force TCP |

## Related Notes

- [[Commands/nslookup|nslookup]]
- [[Dns]]
- [[Commands/ping|ping]]
