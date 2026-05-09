# Lesson 18 Lab — Solutions

1. List block devices in tree view.
```bash
lsblk
```

2. List block devices with filesystem and UUID.
```bash
lsblk -f
```

3. Create a partition using fdisk.
```bash
sudo fdisk /dev/sdb
# n → new partition → p → primary → accept defaults → w to write
```

4. Create XFS filesystem.
```bash
sudo mkfs.xfs /dev/sdb1
```

5. Create mount point.
```bash
sudo mkdir /data
```

6. Mount partition temporarily.
```bash
sudo mount /dev/sdb1 /data
```

7. Verify the mount.
```bash
findmnt /data
```

8. Get UUID of `/dev/sdb1`.
```bash
blkid /dev/sdb1
```

9. Add to `/etc/fstab` (replace UUID with actual value).
```bash
# Add this line to /etc/fstab:
UUID=your-uuid-here  /data  xfs  defaults  0  0
```

10. Test fstab entry.
```bash
sudo umount /data
sudo mount -a
findmnt /data
```

11. Create and activate swap.
```bash
sudo mkswap /dev/sdb2
sudo swapon /dev/sdb2
swapon --show
```
