# Lesson 20 Lab — Solutions

1. Display current default target.
```bash
systemctl get-default
```

2. Change default to `multi-user.target`.
```bash
sudo systemctl set-default multi-user.target
```

3. Switch to rescue target immediately.
```bash
sudo systemctl isolate rescue.target
```

4. Switch back to multi-user.
```bash
sudo systemctl isolate multi-user.target
```

5. List all active targets.
```bash
systemctl list-units --type=target
```

6. GRUB2 config file location (BIOS).
```
/boot/grub2/grub.cfg
```

7. Regenerate GRUB2 config.
```bash
sudo grub2-mkconfig -o /boot/grub2/grub.cfg
```

8. Steps to boot into emergency.target at GRUB:
```
1. Restart the system
2. At the GRUB menu, press 'e' to edit the boot entry
3. Find the line starting with 'linux'
4. At the end of that line, add: systemd.unit=emergency.target
5. Press Ctrl+X to boot with the changes
```
