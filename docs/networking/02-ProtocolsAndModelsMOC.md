---
id: 02-ProtocolsAndModelsMOC
aliases: []
tags: []
---

# Protocols & Models (MOC)

Transport protocols, the OSI model, and the TCP/IP model.

## Concepts

- [[TcpAndUdp|TCP & UDP]]
- [[OsiModel|OSI Model (7 Layers)]]
- [[TcpIpModel|TCP/IP Model (4 Layers)]]
- [[Dns|DNS]]

## Commands

- [[Commands/ss|ss]] — socket statistics
- [[Commands/netstat|netstat]] — legacy socket stats

## Quick Commands

```bash
# List listening ports
ss -tlnp

# DNS lookup
dig example.com

# Reverse DNS
dig -x 8.8.8.8
```

## Related Notes

- [[00-Networking|Networking Overview]]

## Common ports

| Port | Service |
|---|---|
| 22 | SSH |
| 53 | DNS |
| 80 | HTTP |
| 443 | HTTPS |
| 3306 | MySQL |
| 5432 | PostgreSQL |
