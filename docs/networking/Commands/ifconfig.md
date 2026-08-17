---
id: ifconfig
aliases: []
tags: []
---

# ifconfig

Legacy tool for configuring network interfaces. Replaced by `ip` on modern systems.

## Common commands

```bash
# Show all interfaces
ifconfig -a

# Show specific interface
ifconfig eth0

# Assign IP address
sudo ifconfig eth0 192.168.1.100 netmask 255.255.255.0

# Bring interface up/down
sudo ifconfig eth0 up
sudo ifconfig eth0 down

# Set MTU
sudo ifconfig eth0 mtu 1500
```

## Output fields

| Field | Meaning |
|---|---|
| `inet` | IPv4 address |
| `netmask` | Subnet mask |
| `broadcast` | Broadcast address |
| `RX packets` | Packets received |
| `TX packets` | Packets transmitted |

## Notes

- `ifconfig` is deprecated. Use `ip addr` instead.
- Still available on many systems for compatibility.

## Related Notes

- [[Commands/ip|ip]]
- [[IpAddresses]]
- [[Subnetting]]
