---
id: RoutingAndGateways
aliases: []
tags: []
---

# Routing and Gateways

## Router

A device that connects different networks and forwards packets between them based on IP addresses.

### Responsibilities

- Connect different networks
- Forward IP packets
- Maintain routing tables
- Choose the best path
- Perform NAT (often)

### OSI layer

Operates at Layer 3 (Network).

## Gateway

An entry/exit point between networks. The **default gateway** is the router your device sends traffic to when the destination is outside the local network.

```
IP Address:       192.168.1.10
Subnet Mask:      255.255.255.0
Default Gateway:  192.168.1.1
```

Traffic to `192.168.1.x` goes directly. Everything else goes to `192.168.1.1`.

## Routing table

```bash
# View routing table
ip route show
# or
route -n
```

| Destination | Gateway | Interface |
|---|---|---|
| 192.168.1.0/24 | 0.0.0.0 | eth0 (direct) |
| 0.0.0.0/0 | 192.168.1.1 | eth0 (default route) |

## Static vs dynamic routing

| Type | Description |
|---|---|
| Static | Manually configured routes |
| Dynamic | Protocols (OSPF, BGP) learn routes automatically |

## Related Notes

- [[IpAddresses]]
- [[Subnetting]]
- [[NatAndPAT]]
