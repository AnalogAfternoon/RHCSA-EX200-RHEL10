# Lesson 6 Lab — Solutions

---

1. Run `dnf update` as root without switching users.
```bash
sudo dnf update
```

2. Switch fully to root, verify, then return.
```bash
sudo su -
whoami
# Output: root
exit
```

3. Switch to another user.
```bash
su username
```

4. Connect to a remote machine via SSH.
```bash
ssh user@YOUR_SERVER_IP
```

5. Copy `notes.txt` to remote machine.
```bash
scp notes.txt user@YOUR_SERVER_IP:/home/user/
```

6. Copy `remotefile.txt` from remote to local.
```bash
scp user@YOUR_SERVER_IP:/home/user/remotefile.txt .
```
