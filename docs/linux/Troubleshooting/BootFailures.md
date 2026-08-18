---
id: BootFailures
aliases: []
tags: []
---

# Boot Failures — Troubleshooting

Diagnosing and recovering from boot problems.

## Boot Stages

1. **BIOS/UEFI** → 2. **Bootloader** (GRUB) → 3. **Kernel** → 4. **initramfs** → 5. **systemd**

## Common Issues

### GRUB Problems

```bash
# Boot from live USB, chroot
mount /dev/sda1 /mnt
mount /dev/sda2 /mnt/boot
mount --bind /dev /mnt/dev
mount --bind /proc /mnt/proc
mount --bind /sys /mnt/sys
chroot /mnt

# Reinstall GRUB
grub-install /dev/sda
update-grub
```

### Kernel Panic

```bash
# Boot into older kernel from GRUB menu
# Or use recovery mode

# Check kernel logs
journalctl -b -1                            # Previous boot
dmesg | tail -50
```

### Filesystem Errors

```bash
# Boot to recovery/single-user mode
# Run fsck
fsck -y /dev/sda1

# Or force check after reboot
touch /forcefsck
reboot
```

## Recovery Mode

```bash
# GRUB → Advanced → Recovery mode
# Options:
# - Clean: free disk space
# - Fsck: check filesystem
# - Root: root shell
# - Systemctl: disable failed services
```

## Related Notes

- [[RecoveryModes]] — Recovery procedures
- [[SystemdAndInit]] — Boot process
- [[SystemStatus]] — System investigation
- [[DiskManagement]] — Filesystem repair
