---
id: DiskManagement
aliases: []
tags: []
---

# Disk Management

Managing disks, partitions, filesystems, and mount points.

## Identify Disks

```bash
lsblk                                      # Block device tree
lsblk -f                                    # With filesystem info
fdisk -l                                    # Partition tables
blkid                                       # UUID and type
df -h                                       # Mounted filesystem usage
du -sh /path                                # Directory size
```

## Partitioning

```bash
fdisk /dev/sdb                              # MBR partitioning (BIOS)
gdisk /dev/sdb                              # GPT partitioning (UEFI)
parted /dev/sdb                             # Both MBR and GPT
```

## Create Filesystem

```bash
mkfs.ext4 /dev/sdb1                         # ext4 (Linux default)
mkfs.xfs /dev/sdb2                          # XFS (large files)
mkfs.vfat /dev/sdb3                         # FAT32 (USB/EFI)
```

## Mounting

```bash
mount /dev/sdb1 /mnt/data                   # Temporary mount
umount /mnt/data                            # Unmount
mount -o loop disk.iso /mnt/iso             # Mount ISO
```

## Persistent Mounts (/etc/fstab)

```
# <device>  <mount>  <type>  <options>  <dump>  <pass>
UUID=abc123  /data  ext4  defaults  0  2
```

## LVM (Logical Volume Manager)

```bash
pvcreate /dev/sdb                           # Create physical volume
vgcreate data_vg /dev/sdb                   # Create volume group
lvcreate -L 50G -n data_lv data_vg          # Create logical volume
mkfs.ext4 /dev/data_vg/data_lv             # Format
mount /dev/data_vg/data_lv /data            # Mount
```

## Related Notes

- [[FilesystemHierarchy]] — Directory layout
- [[LinuxPermissions]] — Permissions
- [[DiskFull]] — Troubleshooting disk space
- [[BackupAndRestore]] — Backup workflows
