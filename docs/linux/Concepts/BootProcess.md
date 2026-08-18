---
id: BootProcess
aliases: []
tags: []
---

# Boot Process

The sequence from power-on to a working system.

## Boot Stages

| Stage | What Happens |
|-------|-------------|
| 1. Firmware | BIOS/UEFI hardware check, find boot device |
| 2. Bootloader | GRUB loads kernel and initramfs |
| 3. Kernel | Detects hardware, mounts root filesystem |
| 4. Init | systemd (PID 1) starts services |
| 5. Target | Reaches default target (multi-user/graphical) |

## Bootloader (GRUB)

```bash
grub-mkconfig -o /boot/grub/grub.cfg        # Regenerate GRUB config (Arch)
update-grub                                  # Regenerate (Debian/Ubuntu)
```

## Kernel & Initramfs

```bash
ls /boot/                                    # Kernel and initramfs files
dmesg                                        # Kernel boot messages
dmesg | grep -i error                        # Boot errors
journalctl -b                                # Logs from current boot
journalctl -b -1                             # Logs from previous boot
```

## systemd Startup

```bash
systemd-analyze                              # Boot time analysis
systemd-analyze blame                        # Time per service
systemd-analyze critical-chain               # Critical path
```

## Recovery

```bash
# Boot into recovery mode
# 1. Hold Shift during boot (BIOS) or press Esc (UEFI)
# 2. Select "Advanced options" → recovery mode

# Reset root password
# 1. Boot into single-user mode
# 2. mount -o remount,rw /
# 3. passwd root
```

## Related Notes

- [[SystemdAndInit]] — systemd service management
- [[RecoveryModes]] — Recovery troubleshooting
- [[BootFailures]] — Boot troubleshooting
