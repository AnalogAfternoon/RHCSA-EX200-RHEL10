# Lesson 23 — Automating with Bash Scripts

## Overview

Bash scripting lets you automate repetitive tasks by writing sequences of commands into reusable files. This lesson covers the core building blocks of shell scripting — variables, conditionals, and loops.

## Subtopics

- 23.1 Bash Scripting Basic Components
- 23.2 Using Variables and Positional Parameters
- 23.3 Executing Conditional Code with if and test
- 23.4 Using for and while


## Basic Script Structure

```bash
#!/bin/bash
# This is a comment
echo "Hello, World!"
```

- The first line `#!/bin/bash` is called the **shebang** — it tells the system which interpreter to use
- Make a script executable: `chmod +x script.sh`
- Run a script: `./script.sh` or `bash script.sh`

## Variables and Positional Parameters

```bash
# Defining variables (no spaces around =)
NAME="Jason"
echo "Hello, $NAME"

# Positional parameters — arguments passed to the script
echo "Script name: $0"
echo "First argument: $1"
echo "Second argument: $2"
echo "All arguments: $@"
echo "Number of arguments: $#"
```

## Conditional Code — if and test

```bash
# Basic if statement
if [ condition ]; then
  commands
elif [ other_condition ]; then
  commands
else
  commands
fi
```

### Common Test Conditions

| Condition | Meaning |
|-----------|---------|
| `[ -f file ]` | File exists and is a regular file |
| `[ -d dir ]` | Directory exists |
| `[ -z "$var" ]` | Variable is empty |
| `[ -n "$var" ]` | Variable is not empty |
| `[ "$a" = "$b" ]` | Strings are equal |
| `[ "$a" != "$b" ]` | Strings are not equal |
| `[ $a -eq $b ]` | Numbers are equal |
| `[ $a -gt $b ]` | Number a is greater than b |
| `[ $a -lt $b ]` | Number a is less than b |

### Example

```bash
#!/bin/bash
if [ -f /etc/passwd ]; then
  echo "passwd file exists"
else
  echo "passwd file not found"
fi
```

## Loops

### for Loop

```bash
# Loop over a list
for item in one two three; do
  echo "Item: $item"
done

# Loop over files
for file in /etc/*.conf; do
  echo "Config file: $file"
done

# Loop with a range
for i in {1..5}; do
  echo "Number: $i"
done
```

### while Loop

```bash
COUNT=1
while [ $COUNT -le 5 ]; do
  echo "Count: $COUNT"
  COUNT=$((COUNT + 1))
done
```

---

## Useful Script Features

```bash
# Read user input
read -p "Enter your name: " NAME
echo "Hello, $NAME"

# Command output into a variable
HOSTNAME=$(hostname)
echo "Running on: $HOSTNAME"

# Exit codes
exit 0   # Success
exit 1   # Failure
```

## Key Takeaway

For the RHCSA, know how to write a basic script with a shebang, use variables, write an `if` statement with `[ ]` test conditions, and build a `for` loop. Practice writing small utility scripts — the exam may ask you to create one from scratch.
