# Lesson 18 — Working with Partitions and Mounts

## Overview

Storage management is a major RHCSA topic. This lesson covers how disk layout works in Linux, how to create and manage partitions, and how to mount filesystems both temporarily and permanently.

## Subtopics

- 18.1 Understanding Disk Layout
- 18.2 Listing Block Devices
- 18.3 Understanding GPT and MBR Partitions
- 18.4 Creating Partitions
- 18.5 Creating and Mounting Filesystems
- 18.6 Mounting Partitions through /etc/fstab
- 18.7 Using UUID and Labels
- 18.8 Defining Systemd Mounts
- 18.9 Creating a Swap Partition

## Listing Block Devices

| Command | Description |
|--------|-------------|
| `lsblk` | List all block devices in a tree view |
| `lsblk -f` | Show filesystem type and UUID for each device |
| `fdisk -l` | List all disks and their partitions |
| `blkid` | Show UUIDs and labels for all block devices |

## Partition Table Types

| Type | Description |
|------|-------------|
| MBR (msdos) | Older format — max 4 primary partitions, max 2TB disk |
| GPT | Modern format — up to 128 partitions, supports large disks |

## Creating Partitions

### fdisk — MBR Partitions

```bash
fdisk /dev/sdb
# Opens the interactive partitioning tool
```

| Key inside fdisk | Action |
|-----------------|--------|
| `n` | New partition |
| `p` | Primary partition |
| `d` | Delete partition |
| `l` | List partition types |
| `t` | Change partition type |
| `w` | Write changes and exit |
| `q` | Quit without saving |

### gdisk — GPT Partitions

```bash
gdisk /dev/sdb
# Opens GPT partition tool — same key layout as fdisk
```

## Creating Filesystems

| Command | Description |
|--------|-------------|
| `mkfs.xfs /dev/sdb1` | Create an XFS filesystem (default on RHEL) |
| `mkfs.ext4 /dev/sdb1` | Create an ext4 filesystem |
| `mkswap /dev/sdb2` | Prepare a swap partition |


## Mounting Filesystems

| Command | Description |
|--------|-------------|
| `mount /dev/sdb1 /mnt` | Mount a partition to /mnt |
| `umount /mnt` | Unmount a filesystem |
| `mount -a` | Mount everything listed in /etc/fstab |
| `findmnt` | Show all currently mounted filesystems |


## /etc/fstab — Persistent Mounts

Entries in `/etc/fstab` are mounted automatically at boot.

```
# Device        Mount Point   Type   Options    Dump  Pass
/dev/sdb1       /data         xfs    defaults   0     0
UUID=xxxx-xxxx  /backup       ext4   defaults   0     2
```

| Field | Description |
|-------|-------------|
| Device | Device file, UUID, or label |
| Mount Point | Where to mount it |
| Type | Filesystem type (xfs, ext4, swap) |
| Options | Mount options (defaults is standard) |
| Dump | 0 = no backup by dump |
| Pass | Filesystem check order (0=skip, 1=root, 2=others) |


## UUID and Labels

Using UUIDs is safer than device names because device names can change.

```bash
blkid /dev/sdb1
# Output: /dev/sdb1: UUID="abc-123" TYPE="xfs"

# Use in fstab:
UUID=abc-123  /data  xfs  defaults  0  0

# Assign a label:
xfs_admin -L "mydata" /dev/sdb1

# Use label in fstab:
LABEL=mydata  /data  xfs  defaults  0  0
```

## Systemd Mount Units

An alternative to fstab — create a `.mount` unit file:

```ini
[Unit]
Description=Mount /data

[Mount]
What=/dev/sdb1
Where=/data
Type=xfs

[Install]
WantedBy=multi-user.target
```

File must be named to match the mount point: `/etc/systemd/system/data.mount`

## Swap Partition

```bash
mkswap /dev/sdb2
# Prepares the swap partition

swapon /dev/sdb2
# Activates swap immediately

swapoff /dev/sdb2
# Deactivates swap

swapon --show
# Shows all active swap spaces

free -h
# Shows swap usage in the memory output
```

Add to `/etc/fstab` for persistent swap:
```
/dev/sdb2   swap   swap   defaults   0   0
```

## Key Takeaway

Partitions and mounts are heavily tested on the RHCSA. Know `lsblk`, `fdisk`, `mkfs.xfs`, `mount`, and `/etc/fstab` format. Always use UUIDs in fstab for reliability. Know how to create and activate swap. A wrong fstab entry can prevent the system from booting — always double-check your entries.
