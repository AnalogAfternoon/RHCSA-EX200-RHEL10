# Lesson 25 Lab — Solutions

1. Install Apache.
```bash
sudo dnf install httpd -y
```

2. Enable and start `httpd`.
```bash
sudo systemctl enable --now httpd
```

3. Verify Apache is running.
```bash
systemctl status httpd
```

4. Create index page.
```bash
echo "Welcome to my RHEL web server" | sudo tee /var/www/html/index.html
```

5. Open firewall for HTTP.
```bash
sudo firewall-cmd --permanent --add-service=http
sudo firewall-cmd --reload
```

6. Test config for syntax errors.
```bash
sudo httpd -t
```

7. Check SELinux context.
```bash
ls -Z /var/www/html/
```

8. Move file and restore SELinux context.
```bash
sudo mv /tmp/mypage.html /var/www/html/
sudo restorecon -v /var/www/html/mypage.html
```

9. View Apache error log.
```bash
sudo tail -f /var/log/httpd/error_log
```

10. Reload Apache.
```bash
sudo systemctl reload httpd
```
