---
id: ConnectivityIssues
aliases: []
tags: []
---

# Connectivity Issues

Diagnosing when a host cannot reach another host.

## Diagnostic flow

```bash
# 1. Check local interface
ip addr show

# 2. Check if gateway is reachable
ping 192.168.1.1

# 3. Check if remote host is reachable
ping 8.8.8.8

# 4. Check DNS
ping google.com

# 5. Check the route
ip route show
```

## Common causes

| Symptom | Likely cause | Fix |
|---|---|---|
| Can't ping gateway | Physical connection or IP config | Check cable, `ip addr`, `ip route` |
| Can ping gateway but not internet | Default route missing | `ip route add default via 192.168.1.1` |
| Can ping IP but not hostname | DNS issue | See [[DnsResolution]] |
| Intermittent drops | Congestion or cable issue | `ping -c 100` to check loss % |
| Connection refused | Firewall blocking | Check iptables/ufw rules |
| Timeout | Routing issue or firewall | `traceroute` to find where it stops |

## Systematic approach

```
Local interface → Gateway → Internet IP → DNS name → Specific port
```

Test each layer in order until you find the failure point.

## Related Notes

- [[DnsResolution]]
- [[FirewallBlocking]]
- [[Commands/ping|ping]]
- [[Commands/traceroute|traceroute]]
