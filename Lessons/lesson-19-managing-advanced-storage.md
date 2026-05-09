# Lesson 19 — Managing Advanced Storage

## Overview

Beyond basic partitions, RHEL supports advanced storage solutions that offer flexibility, scalability, and snapshots. This lesson covers LVM (Logical Volume Manager) and Stratis, both of which are key RHCSA topics.

## Subtopics

- 19.1 Understanding Advanced Storage Solutions
- 19.2 Exploring LVM Setup
- 19.3 Creating an LVM Logical Volume
- 19.4 Understanding Device Mapper and LVM Device Names
- 19.5 Resizing LVM Logical Volumes
- 19.6 Reducing Volume Groups
- 19.7 Creating Stratis Volumes
- 19.8 Using Stratis Snapshots

## LVM — Logical Volume Manager

LVM adds a layer of abstraction between physical disks and filesystems, allowing you to resize, move, and manage storage flexibly.

### LVM Layers

```
Physical Disks → Physical Volumes (PV) → Volume Groups (VG) → Logical Volumes (LV)
```

## Physical Volumes (PV)

| Command | Description |
|--------|-------------|
| `pvcreate /dev/sdb` | Initialize a disk as a physical volume |
| `pvs` | List all physical volumes |
| `pvdisplay` | Show detailed PV information |
| `pvremove /dev/sdb` | Remove a physical volume |

## Volume Groups (VG)

| Command | Description |
|--------|-------------|
| `vgcreate vgname /dev/sdb` | Create a volume group |
| `vgextend vgname /dev/sdc` | Add a disk to an existing volume group |
| `vgreduce vgname /dev/sdc` | Remove a disk from a volume group |
| `vgs` | List all volume groups |
| `vgdisplay` | Show detailed VG information |
| `vgremove vgname` | Remove a volume group |


## Logical Volumes (LV)

| Command | Description |
|--------|-------------|
| `lvcreate -L 10G -n lvname vgname` | Create a 10GB logical volume |
| `lvcreate -l 100%FREE -n lvname vgname` | Use all free space in the VG |
| `lvs` | List all logical volumes |
| `lvdisplay` | Show detailed LV information |
| `lvremove /dev/vgname/lvname` | Remove a logical volume |


## Creating a Full LVM Setup

```bash
# Step 1 — Create physical volume
pvcreate /dev/sdb

# Step 2 — Create volume group
vgcreate myvg /dev/sdb

# Step 3 — Create logical volume
lvcreate -L 5G -n mylv myvg

# Step 4 — Create filesystem
mkfs.xfs /dev/myvg/mylv

# Step 5 — Mount it
mkdir /data
mount /dev/myvg/mylv /data
```


## Resizing Logical Volumes

### Extend (grow)

```bash
lvextend -L +5G /dev/myvg/mylv
# Adds 5GB to the logical volume

xfs_growfs /data
# Expands XFS filesystem to fill the new space

# For ext4 instead:
resize2fs /dev/myvg/mylv
```

### Reduce (shrink) — ext4 only

```bash
# XFS cannot be shrunk — ext4 can
umount /data
e2fsck -f /dev/myvg/mylv
resize2fs /dev/myvg/mylv 3G
lvreduce -L 3G /dev/myvg/mylv
mount /dev/myvg/mylv /data
```


## Device Mapper and LVM Device Names

LVM volumes appear in two ways — both refer to the same device:

| Format | Example |
|--------|---------|
| `/dev/vgname/lvname` | `/dev/myvg/mylv` |
| `/dev/mapper/vgname-lvname` | `/dev/mapper/myvg-mylv` |


## Stratis — Modern Storage Management

Stratis is a newer storage management tool that simplifies creating pools and filesystems with built-in snapshot support.

| Command | Description |
|--------|-------------|
| `stratis pool create poolname /dev/sdb` | Create a Stratis pool |
| `stratis pool list` | List all Stratis pools |
| `stratis pool add-data poolname /dev/sdc` | Add a device to a pool |
| `stratis filesystem create poolname fsname` | Create a filesystem in the pool |
| `stratis filesystem list` | List all Stratis filesystems |
| `stratis filesystem snapshot poolname fsname snapname` | Create a snapshot |
| `stratis filesystem destroy poolname fsname` | Remove a filesystem |
| `stratis pool destroy poolname` | Remove a pool |

### Mounting a Stratis Filesystem

```bash
mount /stratis/poolname/fsname /mountpoint

# In /etc/fstab — must use UUID and x-systemd.requires:
UUID=xxxx  /data  xfs  defaults,x-systemd.requires=stratisd.service  0  0
```


## Key Takeaway

LVM is a guaranteed RHCSA exam topic. Know the full workflow: `pvcreate → vgcreate → lvcreate → mkfs → mount`. Know how to extend a volume with `lvextend` and `xfs_growfs`. For Stratis, know how to create pools, filesystems, and snapshots. Remember XFS cannot be shrunk — only extended.
