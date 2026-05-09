# Lesson 5 Lab — Solutions

---

1. Search for "root" in `/etc/passwd`.
```bash
grep "root" /etc/passwd
```

2. Show lines NOT containing "nologin".
```bash
grep -v "nologin" /etc/passwd
```

3. Count lines containing "bash".
```bash
grep -c "bash" /etc/passwd
```

4. Lines beginning with "root".
```bash
grep "^root" /etc/passwd
```

5. Case-insensitive search for "ROOT".
```bash
grep -i "ROOT" /etc/passwd
```

6. Recursive search for "sshd" in `/etc`.
```bash
grep -r "sshd" /etc
```

7. Lines containing any digit.
```bash
grep "[0-9]" /etc/passwd
```

8. Files ending in `.conf`.
```bash
ls /etc | grep "\.conf$"
```
