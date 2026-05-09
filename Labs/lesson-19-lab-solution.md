# Lesson 19 Lab — Solutions

1. Initialize physical volume.
```bash
sudo pvcreate /dev/sdb
```

2. Create volume group.
```bash
sudo vgcreate myvg /dev/sdb
```

3. Create logical volume.
```bash
sudo lvcreate -L 5G -n mylv myvg
```

4. Create XFS filesystem.
```bash
sudo mkfs.xfs /dev/myvg/mylv
```

5. Mount persistently via fstab.
```bash
sudo mkdir /mnt/data
# Add to /etc/fstab:
/dev/myvg/mylv  /mnt/data  xfs  defaults  0  0
sudo mount -a
```

6. Extend logical volume by 2GB.
```bash
sudo lvextend -L +2G /dev/myvg/mylv
```

7. Grow XFS filesystem.
```bash
sudo xfs_growfs /mnt/data
```

8. List PVs, VGs, and LVs.
```bash
pvs
vgs
lvs
```

9. Create Stratis pool.
```bash
sudo stratis pool create mypool /dev/sdc
```

10. Create Stratis filesystem.
```bash
sudo stratis filesystem create mypool myfs
```

11. List Stratis pools and filesystems.
```bash
stratis pool list
stratis filesystem list
```
