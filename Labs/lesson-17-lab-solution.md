# Lesson 17 Lab — Solutions

1. View all logs from current boot.
```bash
journalctl -b
```

2. View only error messages from current boot.
```bash
journalctl -b -p err
```

3. Follow live journal logs.
```bash
journalctl -f
```

4. View logs for `sshd` only.
```bash
journalctl -u sshd
```

5. View logs from last 30 minutes.
```bash
journalctl --since "30 min ago"
```

6. Send a test message to syslog.
```bash
logger "This is a test message"
```

7. View last 20 lines of `/var/log/messages`.
```bash
tail -n 20 /var/log/messages
```

8. Make journal persistent.
```bash
sudo mkdir -p /var/log/journal
sudo systemctl restart systemd-journald
```

9. Check rsyslog status.
```bash
systemctl status rsyslog
```

10. View logs from previous boot.
```bash
journalctl -b -1
```
