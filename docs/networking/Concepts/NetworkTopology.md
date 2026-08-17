---
id: NetworkTopology
aliases: []
tags: []
---

# Network Topology

The physical or logical layout of devices and connections in a network.

## Types

| Topology | Layout | Pros | Cons |
|---|---|---|---|
| Bus | Single shared cable | Simple, cheap | Single point of failure, hard to troubleshoot |
| Star | All devices → central switch | Easy to manage, isolate faults | Switch is single point of failure |
| Ring | Devices form a circle | Equal access, no collisions | One break disables the ring |
| Mesh | Every device → every device | Redundant, fault-tolerant | Expensive, complex |
| Tree | Hierarchical (branches) | Scalable, organized | Backbone failure affects branches |
| Hybrid | Mix of topologies | Flexible, tailored | Complex design |

## Quick reference

- **Bus** → One shared cable
- **Star** → Everything connects to a central switch
- **Ring** → Devices form a circle
- **Mesh** → Everyone connects to everyone
- **Tree** → Hierarchical branches
- **Hybrid** → Combination of multiple topologies

## Common in practice

| Environment | Typical topology |
|---|---|
| Home network | Star (router = central switch) |
| Office | Star (switches + VLANs) |
| Data center | Leaf-spine (mesh variant) |
| WAN | Partial mesh |

## Related Notes

- [[OsiModel]]
- [[RoutingAndGateways]]
- [[DataTransmission]]
