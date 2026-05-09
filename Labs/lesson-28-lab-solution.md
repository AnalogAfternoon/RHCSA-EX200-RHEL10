# Lesson 28 Lab — Solutions

1. Check firewalld status.
```bash
systemctl status firewalld
```

2. Display all current firewall rules.
```bash
sudo firewall-cmd --list-all
```

3. Show listening ports with processes.
```bash
ss -tulnp
```

4. Allow `http` service permanently.
```bash
sudo firewall-cmd --permanent --add-service=http
```

5. Allow `https` service permanently.
```bash
sudo firewall-cmd --permanent --add-service=https
```

6. Reload the firewall.
```bash
sudo firewall-cmd --reload
```

7. Allow port `8080/tcp` permanently.
```bash
sudo firewall-cmd --permanent --add-port=8080/tcp
sudo firewall-cmd --reload
```

8. List allowed services.
```bash
sudo firewall-cmd --list-services
```

9. List allowed ports.
```bash
sudo firewall-cmd --list-ports
```

10. Remove `http` service permanently.
```bash
sudo firewall-cmd --permanent --remove-service=http
sudo firewall-cmd --reload
```

11. Add rich rule for SSH from specific network.
```bash
sudo firewall-cmd --permanent --add-rich-rule='rule family="ipv4" source address="192.168.1.0/24" service name="ssh" accept'
sudo firewall-cmd --reload
```

12. Verify all rules.
```bash
sudo firewall-cmd --list-all
```
