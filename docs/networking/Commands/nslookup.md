---
id: nslookup
aliases: []
tags: []
---

# nslookup

Query DNS servers to resolve hostnames or look up DNS records.

## Basic usage

```bash
# Resolve hostname
nslookup example.com

# Resolve with specific DNS server
nslookup example.com 8.8.8.8

# Reverse lookup (IP → name)
nslookup 93.184.216.34
```

## Interactive mode

```bash
nslookup
> server 8.8.8.8
> set type=MX
> example.com
> exit
```

## Record types

```bash
nslookup -type=A example.com
nslookup -type=MX example.com
nslookup -type=TXT example.com
nslookup -type=CNAME www.example.com
```

## Notes

- `nslookup` is being deprecated in favor of `dig`.
- `dig` provides more detailed output and better scripting support.

## Related Notes

- [[Commands/dig|dig]]
- [[Dns]]
- [[Commands/ping|ping]]
