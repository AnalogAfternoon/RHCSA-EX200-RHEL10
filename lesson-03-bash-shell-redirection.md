# Lesson 3 — Bash Shell Redirection

## Overview

By default, commands print their output to the screen. Redirection lets you control where that output goes — into a file, into another command, or thrown away entirely. This is one of the most powerful concepts in Linux.

## Redirection Operators

| Operator | Description |
|---------|-------------|
| `>` | Overwrite — send output to a file (replaces existing content) |
| `>>` | Append — add output to the end of a file |
| `\|` | Pipe — send output of one command into another command |
| `2>` | Redirect error messages to a file |
| `2>/dev/null` | Discard error messages entirely |
| `2>&1` | Redirect errors to the same destination as standard output |

## Viewing Output

| Command | Description |
|--------|-------------|
| `head -n` | Show the first n lines of a file or output |
| `tail -n` | Show the last n lines of a file or output |
| `less` | Scroll through long output interactively (q to quit) |

## Examples

```bash
ls > filelist.txt
# Saves the directory listing to a file instead of the screen

echo "new line" >> filelist.txt
# Appends a line to the file without overwriting it

ls /etc | less
# Pipes the long /etc listing into less so you can scroll it

ls /fakedir 2>/dev/null
# Hides the "No such file" error message

ls /fakedir 2> errors.txt
# Saves the error message to a file instead

command > output.txt 2>&1
# Sends both normal output and errors into the same file
```


## Key Takeaway

Redirection is what makes Linux scripting powerful. The pipe `|` is especially important — it lets you chain commands together. For the RHCSA, know the difference between `>` (overwrite) and `>>` (append), and understand `2>&1` for capturing all output including errors.
