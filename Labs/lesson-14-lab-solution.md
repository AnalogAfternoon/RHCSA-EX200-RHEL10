# Lesson 14 Lab — Solutions

---

1. Run `sleep 500` in background.
```bash
sleep 500 &
# Note the PID shown in brackets
```

2. Gracefully terminate by PID.
```bash
kill PID
```

3. Force kill with SIGKILL.
```bash
sleep 500 &
kill -9 PID
```

4. Kill all `sleep` processes.
```bash
killall sleep
```

5. Start tar with lower priority.
```bash
nice -n 10 tar -czf /tmp/test.tar.gz /etc
```

6. Change priority of running process.
```bash
renice 5 -p PID
```

7. List tuned profiles.
```bash
tuned-adm list
```

8. Show active tuned profile.
```bash
tuned-adm active
```

9. Apply `balanced` profile.
```bash
sudo tuned-adm profile balanced
```

10. Show logged-in users and activity.
```bash
w
```
