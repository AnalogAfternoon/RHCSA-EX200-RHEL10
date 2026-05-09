# Lesson 26 Lab — Solutions

---

1. Display current time and NTP status.
```bash
timedatectl
```

2. List timezones containing "America".
```bash
timedatectl list-timezones | grep America
```

3. Set timezone to `America/New_York`.
```bash
sudo timedatectl set-timezone America/New_York
```

4. Display current date and time.
```bash
date
```

5. Check chronyd status.
```bash
systemctl status chronyd
```

6. Display NTP sync status and sources.
```bash
chronyc tracking
chronyc sources
```

7. Force immediate time sync.
```bash
sudo chronyc makestep
```

8. Add NTP server and restart chronyd.
```bash
sudo vim /etc/chrony.conf
# Add the line: server pool.ntp.org iburst
sudo systemctl restart chronyd
```

9. Enable NTP synchronization.
```bash
sudo timedatectl set-ntp true
```

10. Verify NTP is active.
```bash
timedatectl
# Look for: System clock synchronized: yes
#           NTP service: active
```
