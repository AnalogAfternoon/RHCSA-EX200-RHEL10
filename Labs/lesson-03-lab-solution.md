# Lesson 3 Lab — Solutions

---

1. Save `ls /etc` output to `etclist.txt`.
```bash
ls /etc > etclist.txt
```

2. Append `ls /etc` output to `etclist.txt`.
```bash
ls /etc >> etclist.txt
```

3. Redirect error from `ls /fakedir` to `errors.txt`.
```bash
ls /fakedir 2> errors.txt
```

4. Discard error message entirely.
```bash
ls /fakedir 2>/dev/null
```

5. Display first 5 lines of `etclist.txt`.
```bash
head -n 5 etclist.txt
```

6. Display last 5 lines of `etclist.txt`.
```bash
tail -n 5 etclist.txt
```

7. Pipe `ls /etc` into `less`.
```bash
ls /etc | less
# Press q to quit
```

8. Send both stdout and stderr to `all-output.txt`.
```bash
ls /etc /fakedir > all-output.txt 2>&1
```
