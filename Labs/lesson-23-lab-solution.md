# Lesson 23 Lab — Solutions

1. `hello.sh`
```bash
#!/bin/bash
echo "Hello, RHCSA!"
```
```bash
chmod +x hello.sh
./hello.sh
```

2. `args.sh`
```bash
#!/bin/bash
echo "First argument: $1"
echo "Second argument: $2"
```

3. `check-file.sh`
```bash
#!/bin/bash
if [ -f /etc/passwd ]; then
  echo "File exists"
else
  echo "File not found"
fi
```

4. `check-root.sh`
```bash
#!/bin/bash
if [ "$EUID" -eq 0 ]; then
  echo "Running as root."
else
  echo "Not root."
fi
```

5. `counter.sh`
```bash
#!/bin/bash
for i in {1..5}; do
  echo "Number: $i"
done
```

6. `whilecount.sh`
```bash
#!/bin/bash
COUNT=5
while [ $COUNT -ge 1 ]; do
  echo "Count: $COUNT"
  COUNT=$((COUNT - 1))
done
```
