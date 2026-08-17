---
id: Subnetting
aliases: []
tags: []
---

# Subnetting

Subnetting divides a larger network into smaller sub-networks (subnets) by borrowing bits from the host portion of an IP address.

## Subnet mask

A 32-bit number that separates the network and host portions of an IP address.

```
IP:     192.168.1.10
Mask:   255.255.255.0
Network: 192.168.1.0
Host:   .10
```

## CIDR notation

Classless Inter-Domain Routing uses a slash prefix to indicate how many bits are the network portion.

```
192.168.1.0/24    → 255.255.255.0
10.0.0.0/8        → 255.0.0.0
172.16.0.0/12     → 255.240.0.0
```

## Common CIDR blocks

| CIDR | Subnet mask | Hosts | Use case |
|---|---|---|---|
| /32 | 255.255.255.255 | 1 | Single host |
| /24 | 255.255.255.0 | 254 | Small LAN |
| /16 | 255.255.0.0 | 65,534 | Medium network |
| /8 | 255.0.0.0 | 16M+ | Large enterprise |

## Broadcast address

The last address in a subnet — used to send data to all hosts.

```
Network:    192.168.1.0/24
Range:      192.168.1.0 – 192.168.1.255
Broadcast:  192.168.1.255
```

## Calculate subnets

```bash
# How many subnets from a /24 split into /26?
# /26 = 64 hosts per subnet
# 256 / 64 = 4 subnets

# Subnets:
# 192.168.1.0/26    (hosts: .1 – .62,   broadcast: .63)
# 192.168.1.64/26   (hosts: .65 – .126, broadcast: .127)
# 192.168.1.128/26  (hosts: .129 – .190, broadcast: .191)
# 192.168.1.192/26  (hosts: .193 – .254, broadcast: .255)
```

## Related Notes

- [[IpAddresses]]
- [[NatAndPAT]]
- [[RoutingAndGateways]]
