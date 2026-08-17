---
id: RoutingTables
aliases: []
tags: []
---

# Routing Tables

How the kernel decides where to send network packets.

## View Routing Table

```bash
ip route show                              # Modern route display
route -n                                   # Legacy route display
netstat -rn                                # Alternative view
```

## Route Types

| Route Type | Purpose |
|------------|---------|
| Default | Gateway for unmatched destinations |
| Network | Route to a specific subnet |
| Host | Route to a specific host |
| Connected | Directly attached network |

## Add Routes

```bash
sudo ip route add 10.0.0.0/8 via 192.168.1.1    # Add static route
sudo ip route add default via 192.168.1.1        # Set default gateway
sudo ip route del 10.0.0.0/8                     # Delete route
```

## Related Notes

- [[IpAddresses]] — IP addressing
- [[LanSetup]] — LAN configuration
- [[NetworkInterfaces]] — Interface setup
- [[SysctlNetworking]] — Kernel parameters
- [[NetworkPerformance]] — Performance tuning
