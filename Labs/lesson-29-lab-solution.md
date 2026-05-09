# Lesson 29 Lab — Solutions

1. Install `nfs-utils`.
```bash
sudo dnf install nfs-utils -y
```

2. Enable and start NFS server.
```bash
sudo systemctl enable --now nfs-server
```

3. Create shared directory.
```bash
sudo mkdir -p /exports/data
```

4. Edit `/etc/exports`.
```bash
sudo vim /etc/exports
# Add the line:
/exports/data    *(rw,sync)
```

5. Apply export changes.
```bash
sudo exportfs -r
```

6. View active exports.
```bash
sudo exportfs -v
```

7. Open firewall for NFS.
```bash
sudo firewall-cmd --permanent --add-service=nfs
sudo firewall-cmd --permanent --add-service=rpcbind
sudo firewall-cmd --reload
```

8. Show server exports from client.
```bash
showmount -e YOUR_SERVER_IP
```

9. Mount NFS share temporarily.
```bash
sudo mkdir -p /mnt/nfsdata
sudo mount YOUR_SERVER_IP:/exports/data /mnt/nfsdata
```

10. Add to `/etc/fstab` for persistence.
```bash
# Add this line to /etc/fstab:
YOUR_SERVER_IP:/exports/data  /mnt/nfsdata  nfs  defaults  0  0
```

11. Install and enable autofs.
```bash
sudo dnf install autofs -y
sudo systemctl enable --now autofs
```

12. Configure autofs for `/misc/data`.
```bash
# Edit /etc/auto.master and add:
/misc   /etc/auto.misc

# Edit /etc/auto.misc and add:
data    -rw,sync    YOUR_SERVER_IP:/exports/data

sudo systemctl restart autofs
# Test by running: cd /misc/data
```
