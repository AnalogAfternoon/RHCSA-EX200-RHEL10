# Lesson 27 Lab — Solutions

---

1. Display current SELinux mode.
```bash
getenforce
```

2. Switch to permissive mode temporarily.
```bash
sudo setenforce 0
```

3. Switch back to enforcing mode.
```bash
sudo setenforce 1
```

4. Display SELinux context of `/var/www/html/`.
```bash
ls -Z /var/www/html/
```

5. Display SELinux context of `sshd` process.
```bash
ps -eZ | grep sshd
```

6. Move file and restore context.
```bash
touch /tmp/webfile.html
sudo mv /tmp/webfile.html /var/www/html/
sudo restorecon -v /var/www/html/webfile.html
```

7. List context rules for `/var/www`.
```bash
semanage fcontext -l | grep "/var/www"
```

8. Add persistent context rule for `/mywebsite`.
```bash
sudo semanage fcontext -a -t httpd_sys_content_t "/mywebsite(/.*)?"
```

9. Apply the new context rule.
```bash
sudo mkdir -p /mywebsite
sudo restorecon -Rv /mywebsite
```

10. Check `httpd_can_network_connect` boolean.
```bash
getsebool httpd_can_network_connect
```

11. Turn boolean on persistently.
```bash
sudo setsebool -P httpd_can_network_connect on
```

12. View recent SELinux denial messages.
```bash
sudo ausearch -m avc -ts recent
```
