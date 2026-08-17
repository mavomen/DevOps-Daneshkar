---
id: ip
aliases: []
tags: []
---

# ip

Modern replacement for `ifconfig`, `route`, and `arp`. The primary tool for network configuration on Linux.

## ip addr — show/manage addresses

```bash
# Show all interfaces
ip addr show
# or
ip a

# Show specific interface
ip addr show eth0

# Add an IP address
sudo ip addr add 192.168.1.100/24 dev eth0

# Remove an IP address
sudo ip addr del 192.168.1.100/24 dev eth0
```

## ip link — show/manage interfaces

```bash
# Show all interfaces with state
ip link show

# Bring interface up/down
sudo ip link set eth0 up
sudo ip link set eth0 down

# Change MAC address
sudo ip link set eth0 address aa:bb:cc:dd:ee:ff
```

## ip route — show/manage routing

```bash
# Show routing table
ip route show

# Add default gateway
sudo ip route add default via 192.168.1.1

# Add static route
sudo ip route add 10.0.0.0/8 via 192.168.1.254

# Delete route
sudo ip route del 10.0.0.0/8
```

## ip neigh — ARP table

```bash
# Show ARP table
ip neigh show

# Add static ARP entry
sudo ip neigh add 192.168.1.20 lladdr aa:bb:cc:dd:ee:ff dev eth0
```

## ifconfig vs ip

| Task | ifconfig | ip |
|---|---|---|
| Show addresses | `ifconfig -a` | `ip a` |
| Show interfaces | `ifconfig` | `ip link` |
| Show routes | `route -n` | `ip route` |
| Show ARP | `arp -n` | `ip neigh` |

## Related Notes

- [[Commands/ifconfig|ifconfig]]
- [[IpAddresses]]
- [[Subnetting]]
- [[RoutingAndGateways]]
