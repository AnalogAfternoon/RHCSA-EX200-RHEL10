# Lesson 29 — Using Remote Filesystems and Autofs

## Overview

Linux can mount filesystems from remote servers over the network using NFS. Autofs takes this further by automatically mounting remote filesystems only when they are accessed, saving resources.

## Subtopics

- 29.1 Configuring a Base NFS Server
- 29.2 Mounting NFS Shares
- 29.3 Configuring Automount
- 29.4 Setting up Autofs for Home Directories
- 29.5 Using Systemd Automount Services


## NFS — Network File System

### Setting Up an NFS Server

```bash
# Install NFS server package
dnf install nfs-utils

# Enable and start NFS
systemctl enable --now nfs-server

# Create the directory to share
mkdir /shared

# Edit the exports file
vim /etc/exports
```

### /etc/exports Format

```
/shared    *(rw,sync,no_root_squash)
/shared    192.168.1.0/24(rw,sync)
```

| Option | Description |
|--------|-------------|
| `rw` | Read and write access |
| `ro` | Read only access |
| `sync` | Write data to disk before confirming |
| `no_root_squash` | Allow remote root to act as root |
| `root_squash` | Map remote root to nobody (default, safer) |

```bash
# Apply export changes without restarting
exportfs -r

# View current exports
exportfs -v

# Open firewall for NFS
firewall-cmd --permanent --add-service=nfs
firewall-cmd --permanent --add-service=rpcbind
firewall-cmd --reload
```

## Mounting NFS Shares (Client Side)

```bash
# Show what a server is exporting
showmount -e YOUR_SERVER_IP

# Mount an NFS share temporarily
mount YOUR_SERVER_IP:/shared /mnt

# Mount persistently via /etc/fstab
YOUR_SERVER_IP:/shared  /mnt/shared  nfs  defaults  0  0
```

## Autofs — Automatic Mounting

Autofs mounts remote filesystems automatically when accessed and unmounts them after a period of inactivity. This is more efficient than static NFS mounts.

### Installing Autofs

```bash
dnf install autofs
systemctl enable --now autofs
```

### Configuration Files

| File | Description |
|------|-------------|
| `/etc/auto.master` | Master map — defines mount points and map files |
| `/etc/auto.misc` | Example indirect map file |

### Setting Up a Basic Automount

**Step 1 — Edit /etc/auto.master:**
```
/misc   /etc/auto.misc
```

**Step 2 — Edit /etc/auto.misc:**
```
data    -rw,sync    YOUR_SERVER_IP:/shared
```

This means: when `/misc/data` is accessed, mount `YOUR_SERVER_IP:/shared` there automatically.

```bash
systemctl restart autofs

# Test — just cd into the directory
cd /misc/data
ls
# Autofs mounts it automatically on access
```

## Autofs for Home Directories

A common use case — automatically mount user home directories from an NFS server.

**In /etc/auto.master:**
```
/home/nfs   /etc/auto.home
```

**In /etc/auto.home:**
```
*   -rw,sync    YOUR_SERVER_IP:/home/&
```

The `*` matches any username and `&` substitutes it in the path — so accessing `/home/nfs/jason` mounts `YOUR_SERVER_IP:/home/jason`.

## Systemd Automount Units

An alternative to autofs using systemd. Create two unit files — a `.mount` and an `.automount`:

**data.automount:**
```ini
[Unit]
Description=Automount /data

[Automount]
Where=/data

[Install]
WantedBy=multi-user.target
```

```bash
systemctl enable --now data.automount
```

## Key Takeaway

For the RHCSA, know how to configure a basic NFS server with `/etc/exports` and `exportfs -r`. Know how to mount NFS shares with `mount` and in `/etc/fstab`. For autofs, know the master map format and how to set up an indirect map. The wildcard (`*`) and substitution (`&`) pattern for home directories is exam-relevant.
