# Lesson 9 Lab — Solutions

---

1. Create `admin1` with home directory and bash shell.
```bash
sudo useradd -m -s /bin/bash admin1
```

2. Add comment to `admin1`.
```bash
sudo usermod -c "Admin User" admin1
```

3. Create `admins` group.
```bash
sudo groupadd admins
```

4. Add `admin1` to `admins`.
```bash
sudo usermod -aG admins admin1
```

5. Display all groups for `admin1`.
```bash
groups admin1
```

6. Set account expiration.
```bash
sudo chage -E 2025-12-31 admin1
```

7. Set minimum password age to 7 days.
```bash
sudo chage -m 7 admin1
```

8. Set warning period to 14 days.
```bash
sudo chage -W 14 admin1
```

9. View `admin1` in `/etc/passwd`.
```bash
grep "admin1" /etc/passwd
```

10. View `admins` in `/etc/group`.
```bash
grep "admins" /etc/group
```
