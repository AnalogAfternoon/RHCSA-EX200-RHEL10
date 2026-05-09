# Lesson 7 Lab — Solutions

---

1. Create user `student1`.
```bash
sudo useradd student1
```

2. Set password for `student1`.
```bash
sudo passwd student1
```

3. Create group `studygroup`.
```bash
sudo groupadd studygroup
```

4. Add `student1` to `studygroup`.
```bash
sudo usermod -aG studygroup student1
```

5. Lock `student1`.
```bash
sudo usermod -L student1
```

6. Unlock `student1`.
```bash
sudo usermod -U student1
```

7. Set password expiry to 90 days.
```bash
sudo chage -M 90 student1
```

8. Display password aging info.
```bash
sudo chage -l student1
```

9. Delete user and home directory.
```bash
sudo userdel -r student1
```

10. Delete the group.
```bash
sudo groupdel studygroup
```
