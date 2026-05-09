# Lesson 21 Lab — Solutions

---

1. Display current kernel version.
```bash
uname -r
```

2. List loaded kernel modules.
```bash
lsmod
```

3. Display info about `xfs` module.
```bash
modinfo xfs
```

4. Load `xfs` module.
```bash
sudo modprobe xfs
```

5. Remove `xfs` module.
```bash
sudo modprobe -r xfs
```

6. Load `xfs` at boot automatically.
```bash
echo "xfs" | sudo tee /etc/modules-load.d/xfs.conf
```

7. Display `ip_forward` value.
```bash
sysctl net.ipv4.ip_forward
```

8. Enable IP forwarding temporarily.
```bash
sudo sysctl -w net.ipv4.ip_forward=1
```

9. Make IP forwarding persistent.
```bash
echo "net.ipv4.ip_forward = 1" | sudo tee /etc/sysctl.d/99-ipforward.conf
```

10. Apply config without rebooting.
```bash
sudo sysctl -p
```

11. List installed kernel versions.
```bash
dnf list installed kernel
```
