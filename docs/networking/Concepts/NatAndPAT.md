---
id: NatAndPAT
aliases: []
tags: []
---

# NAT and PAT

Network Address Translation translates IP addresses as packets cross network boundaries. PAT (Port Address Translation) extends NAT by using port numbers.

## Why NAT

- Private IPs (`10.x`, `172.16-31.x`, `192.168.x`) cannot be routed on the internet.
- NAT translates private → public at the router.
- Conserves public IPv4 addresses.
- Hides internal network structure.

## Types

| Type | Description |
|---|---|
| Static NAT | One private IP ↔ one public IP |
| Dynamic NAT | Pool of public IPs, assigned on demand |
| PAT (NAPT) | Many private IPs → one public IP (differentiated by port) |

## PAT example

```
192.168.1.10:4000 → 203.0.113.5:40000
192.168.1.11:4000 → 203.0.113.5:40001
192.168.1.12:4000 → 203.0.113.5:40002
```

All three devices share one public IP, distinguished by port numbers.

## Related Notes

- [[IpAddresses]]
- [[Subnetting]]
- [[RoutingAndGateways]]
- [[Firewall]]
