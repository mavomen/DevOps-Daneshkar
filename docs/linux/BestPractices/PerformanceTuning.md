---
id: PerformanceTuning
aliases: []
tags: []
---

# Performance Tuning — Best Practices

Optimizing Linux system performance.

## Monitor First

```bash
# CPU
top -bn1 | head -5
mpstat -P ALL 1 3

# Memory
free -h
vmstat 1 5

# Disk I/O
iostat -xz 1 3
iotop -o

# Network
ss -s
sar -n DEV 1 3
```

## Kernel Tuning

```bash
# /etc/sysctl.d/99-performance.conf

# Network
net.core.somaxconn=4096
net.ipv4.tcp_max_syn_backlog=4096
net.ipv4.ip_local_port_range=1024 65535

# Memory
vm.swappiness=10
vm.dirty_ratio=15
vm.dirty_background_ratio=5
vm.overcommit_memory=1

# File System
fs.file-max=2097152
fs.inotify.max_user_watches=524288

# Apply
sysctl --system
```

## Systemd Services

```bash
# Increase file descriptor limits
# /etc/systemd/system/myapp.service.d/limits.conf
[Service]
LimitNOFILE=65536
LimitNPROC=4096
```

## Disk Performance

```bash
# Use SSD scheduler
echo none > /sys/block/sda/queue/scheduler

# Disable atime
# /etc/fstab: defaults,noatime

# Check I/O
iostat -x 1
```

## Related Notes

- [[SystemStatus]] — System monitoring
- [[DiskManagement]] — Disk management
- [[ProcessManagement]] — Process tuning
- [[NetworkingBasics]] — Network tuning
