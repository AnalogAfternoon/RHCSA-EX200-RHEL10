# Lesson 22 Lab — Solutions

1. Display failed units.
```bash
systemctl --failed
```

2. View errors from current boot.
```bash
journalctl -b -p err
```

3. View kernel/hardware messages.
```bash
dmesg
```

4. Root password reset procedure using `rd.break`:
```
1. Restart the system
2. At GRUB menu, press 'e' to edit the boot entry
3. Find the line starting with 'linux'
4. Add 'rd.break' at the end of that line
5. Press Ctrl+X to boot
6. At the emergency shell, run:
   mount -o remount,rw /sysroot
   chroot /sysroot
   passwd root
   touch /.autorelabel
   exit
   exit
7. System will reboot and relabel SELinux — this may take a few minutes
```

5. Check and repair filesystem.
```bash
sudo umount /dev/sdb1
sudo fsck /dev/sdb1
```

6. Generate sos report.
```bash
sudo sos report
```

7. View NetworkManager logs.
```bash
journalctl -u NetworkManager -f
```

8. Last 50 lines of messages filtered for errors.
```bash
tail -n 50 /var/log/messages | grep -i "error"
```
