---
id: TroubleshootingPerformance
aliases: []
tags: []
---

# Troubleshooting Network Performance

Diagnose and resolve network performance issues.

## Symptoms → Causes

| Symptom | Likely Cause |
|---------|--------------|
| High latency | Buffer bloat, congestion, distance |
| Packet loss | Congestion, faulty hardware, MTU issues |
| Slow transfers | Window size, bandwidth limits |
| Connection timeouts | Firewall, DNS issues |

## Diagnostic Commands

```bash
ping -c 100 target                         # Measure latency
mtr target                                 # Route analysis with loss
iperf3 -c target                           # Bandwidth test
ss -ti                                     # TCP info and retransmits
```

## Common Fixes

```bash
# TCP tuning
sudo sysctl -w net.core.rmem_max=16777216
sudo sysctl -w net.ipv4.tcp_window_scaling=1

# MTU issues
ping -M do -s 1472 target                  # Test MTU
ip link set eth0 mtu 1400                  # Adjust MTU
```

## Related Notes

- [[NetworkPerformance]] — Performance best practices
- [[SysctlNetworking]] — Kernel parameters
- [[TroubleshootingConnectivity]] — Connectivity issues
