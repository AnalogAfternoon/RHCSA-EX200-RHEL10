# Lesson 11 Lab — Solutions

---

1. Display all IP addresses.
```bash
ip addr
```

2. Show routing table.
```bash
ip route
```

3. Show all network device status.
```bash
nmcli device status
```

4. Show current hostname.
```bash
hostname
```

5. Set hostname permanently.
```bash
sudo hostnamectl set-hostname rhcsa-server.local
```

6. Add entry to `/etc/hosts`.
```bash
echo "192.168.1.50  testserver.local" | sudo tee -a /etc/hosts
```

7. List all connection profiles.
```bash
nmcli connection show
```

8. Configure static IP (replace `enp0s3` with your interface name).
```bash
sudo nmcli connection modify "enp0s3" \
  ipv4.addresses 192.168.1.100/24 \
  ipv4.gateway 192.168.1.1 \
  ipv4.dns 8.8.8.8 \
  ipv4.method manual
```

9. Bring the connection up.
```bash
sudo nmcli connection up "enp0s3"
```

10. Test connectivity.
```bash
ping -c 4 8.8.8.8
ping -c 4 google.com
```
