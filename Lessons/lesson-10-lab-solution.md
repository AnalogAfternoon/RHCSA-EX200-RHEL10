# Lesson 10 Lab — Solutions

---

1. Create directory and group, set group ownership.
```bash
sudo mkdir /project
sudo groupadd devs
sudo chown :devs /project
```

2. Set SGID on `/project`.
```bash
sudo chmod g+s /project
```

3. Set permissions `rwxrwx---`.
```bash
sudo chmod 2770 /project
```

4. Create a file and verify group inheritance.
```bash
sudo touch /project/testfile.txt
ls -l /project/testfile.txt
# Group should show as devs
```

5. Check current umask.
```bash
umask
```

6. Set umask to `027`.
```bash
umask 027
```

7. Create file and verify permissions.
```bash
touch newfile.txt
ls -l newfile.txt
# Should show rw-r----- (640)
```

8. Confirm sticky bit on `/tmp`.
```bash
ls -ld /tmp
# Should show drwxrwxrwt
```

9. Create `/shared` with sticky bit.
```bash
sudo mkdir /shared
sudo chmod 1777 /shared
```

10. Verify sticky bit on `/shared`.
```bash
ls -ld /shared
# Should show drwxrwxrwt
```
