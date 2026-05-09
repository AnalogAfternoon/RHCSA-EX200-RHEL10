# Lesson 25 — Managing HTTP Services

> 📺 *Video coming soon!*

---

## Overview

Apache (httpd) is the standard web server on RHEL. This lesson covers how to install, configure, and run a basic web server — a common task in enterprise Linux environments.

---

## Subtopics

- 25.1 Using Web Servers on RHEL
- 25.2 Exploring HTTP Configuration
- 25.3 Creating a Basic Web Site

---

## Installing Apache

```bash
dnf install httpd
# Installs the Apache web server

systemctl enable --now httpd
# Enables and starts Apache immediately

systemctl status httpd
# Verify it's running
```

---

## Key Configuration Files and Directories

| Path | Description |
|------|-------------|
| `/etc/httpd/conf/httpd.conf` | Main Apache configuration file |
| `/etc/httpd/conf.d/` | Drop-in config directory for additional settings |
| `/var/www/html/` | Default document root — put web files here |
| `/var/log/httpd/access_log` | Access log — shows all requests |
| `/var/log/httpd/error_log` | Error log — shows problems |

---

## Basic httpd.conf Settings

```apache
ServerName www.example.com
DocumentRoot "/var/www/html"
Listen 80
```

After any config change:
```bash
# Test config for syntax errors
httpd -t

# Reload without dropping connections
systemctl reload httpd

# Or full restart
systemctl restart httpd
```

---

## Creating a Basic Web Site

```bash
# Create a simple index page
echo "<h1>Welcome to My RHEL Web Server</h1>" > /var/www/html/index.html

# Set correct permissions
chmod 644 /var/www/html/index.html
chown apache:apache /var/www/html/index.html
```

---

## Firewall — Allow HTTP Traffic

```bash
firewall-cmd --permanent --add-service=http
firewall-cmd --permanent --add-service=https
firewall-cmd --reload
# Opens ports 80 (HTTP) and 443 (HTTPS)
```

---

## SELinux and Apache

SELinux can block Apache if files are in the wrong location or have incorrect contexts.

```bash
# Check SELinux context on web files
ls -Z /var/www/html/

# Restore correct context
restorecon -Rv /var/www/html/

# Allow Apache to connect to the network (if needed)
setsebool -P httpd_can_network_connect on
```

---

## Key Takeaway

For the RHCSA, know how to install and start `httpd`, where the document root is (`/var/www/html/`), and how to open the firewall for HTTP. Remember that SELinux context issues are a common reason Apache can't serve files — always check with `ls -Z` and fix with `restorecon`.
