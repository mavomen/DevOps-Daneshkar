---
id: NetworkPerformance
aliases: []
tags: []
---

# Network Performance

Best practices for optimizing network performance.

## TCP Tuning

```bash
# Increase buffer sizes
sudo sysctl -w net.core.rmem_max=16777216
sudo sysctl -w net.core.wmem_max=16777216

# TCP window scaling
sudo sysctl -w net.ipv4.tcp_window_scaling=1

# Reduce timeouts
sudo sysctl -w net.ipv4.tcp_fin_timeout=15
sudo sysctl -w net.ipv4.tcp_keepalive_time=600
```

## Connection Optimization

```bash
# Increase connection backlog
sudo sysctl -w net.core.somaxconn=4096
sudo sysctl -w net.ipv4.tcp_max_syn_backlog=4096

# Enable TCP fast open
sudo sysctl -w net.ipv4.tcp_fastopen=3
```

## Monitoring

```bash
# Bandwidth monitoring
iftop                                        # Real-time bandwidth
nload                                        # Network traffic
vnstat                                       # Traffic statistics

# Latency testing
ping -c 100 target                           # ICMP latency
mtr target                                   # Route analysis
```

## Common Issues

| Symptom | Likely Cause | Solution |
|---------|--------------|----------|
| High latency | Buffer bloat | QoS, traffic shaping |
| Packet loss | Congestion | Bandwidth upgrade, QoS |
| Slow transfers | Window size | TCP tuning |
| Connection refused | Firewall | Check iptables/ufw |

## Related Notes

- [[SysctlNetworking]] - Kernel parameters
- [[RoutingTables]] - Routing optimization
- [[TroubleshootingPerformance]] - Performance issues
