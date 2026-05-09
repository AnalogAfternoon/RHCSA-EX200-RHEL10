# Lesson 8 Lab — Solutions

---

1. Create `secure.txt`.
```bash
touch ~/secure.txt
```

2. Owner read/write only (numeric).
```bash
chmod 600 ~/secure.txt
```

3. Add execute for owner (symbolic).
```bash
touch ~/run.sh
chmod u+x ~/run.sh
```

4. Set to `rw-r--r--`.
```bash
chmod 644 ~/secure.txt
```

5. Change owner to root.
```bash
sudo chown root ~/secure.txt
```

6. Change group to root.
```bash
sudo chgrp root ~/secure.txt
```

7. Create `shared` directory with `rwxrwx---`.
```bash
mkdir ~/shared
chmod 770 ~/shared
```

8. View permissions in home directory.
```bash
ls -l ~
```
