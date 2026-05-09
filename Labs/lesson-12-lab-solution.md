# Lesson 12 Lab — Solutions

1. Search for `vim`.
```bash
dnf search vim
```

2. Install `vim`.
```bash
sudo dnf install vim -y
```

3. Show info about `vim`.
```bash
dnf info vim
```

4. List all installed packages.
```bash
dnf list installed
```

5. Find which package owns `/etc/passwd`.
```bash
rpm -qf /etc/passwd
```

6. List files installed by `bash`.
```bash
rpm -ql bash
```

7. List all package groups.
```bash
dnf group list
```

8. Show dnf history.
```bash
dnf history
```

9. Remove `vim`.
```bash
sudo dnf remove vim -y
```

10. List enabled repositories.
```bash
dnf repolist
```
