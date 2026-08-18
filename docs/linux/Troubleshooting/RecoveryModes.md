---
id: RecoveryModes
aliases: []
tags: []
---

# Recovery Modes — Troubleshooting

Boot options for system recovery.

## GRUB Recovery Options

| Option | Purpose |
|--------|---------|
| Recovery mode | Minimal boot with repair tools |
| Root shell | Direct root access |
| Single user | Minimal services |
| Emergency | Filesystem mounted read-only |

## Enter Recovery

```bash
# At GRUB menu → Advanced Options → Recovery mode
# Or add to kernel line: single / init=/bin/bash
```

## Recovery Mode Actions

| Menu Option | What It Does |
|-------------|-------------|
| Clean | Free disk space |
| Dpkg | Repair broken packages |
| Fsck | Check filesystems |
| Grub | Reinstall GRUB |
| Network | Enable networking |
| Root | Root shell prompt |
| Systemctl | Disable failed services |
| Safe Graphics | Basic display driver |

## Manual Recovery

```bash
# From recovery root shell
mount -o remount,rw /                      # Remount read-write
fsck -y /dev/sda1                          # Check filesystem
dpkg --configure -a                        # Fix packages
apt --fix-broken install                   # Fix dependencies

# Reinstall GRUB
grub-install /dev/sda
update-grub
```

## Chroot Recovery

```bash
# From live USB
mount /dev/sda1 /mnt
mount /dev/sda2 /mnt/boot                  # If separate /boot
for i in dev dev/pts proc sys run; do mount --bind /$i /mnt/$i; done
chroot /mnt

# Now fix issues
apt update && apt upgrade
passwd root
exit
reboot
```

## Related Notes

- [[BootFailures]] — Boot issues
- [[SystemdAndInit]] — Boot process
- [[SystemStatus]] — System investigation
- [[FilesystemHierarchy]] — FS structure
