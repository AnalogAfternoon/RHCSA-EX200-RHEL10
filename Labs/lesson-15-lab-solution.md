# Lesson 15 Lab — Solutions

---

1. Check `sshd` status.
```bash
systemctl status sshd
```

2. Stop `sshd`.
```bash
sudo systemctl stop sshd
```

3. Start `sshd`.
```bash
sudo systemctl start sshd
```

4. Restart `sshd`.
```bash
sudo systemctl restart sshd
```

5. Enable `sshd` at boot.
```bash
sudo systemctl enable sshd
```

6. Verify `sshd` is enabled.
```bash
systemctl is-enabled sshd
```

7. List all active services.
```bash
systemctl list-units --type=service
```

8. View `sshd` unit file.
```bash
systemctl cat sshd
```

9. Mask `bluetooth`.
```bash
sudo systemctl mask bluetooth
```

10. Unmask `bluetooth`.
```bash
sudo systemctl unmask bluetooth
```

11. List failed units.
```bash
systemctl --failed
```
