# Lesson 2 — Using Essential Tools

## Overview

These are the core tools you will reach for daily — creating files, reading them, editing them, and looking up help. Getting comfortable with Vim and `man` pages early will pay off throughout the entire course.

---

## File Creation & Reading

| Command | Description |
|--------|-------------|
| `touch filename` | Create an empty file |
| `echo "text" > file` | Create a file with text (overwrites existing content) |
| `echo "text" >> file` | Append text to an existing file |
| `cat filename` | Read and display the contents of a file |

---

## Vim Text Editor

Vim is the standard text editor on most Linux systems. It has two main modes — **insert mode** for typing and **normal mode** for commands.

| Command | Description |
|--------|-------------|
| `vim filename` | Open a file in Vim |
| `i` | Enter insert mode — start typing |
| `Esc` | Return to normal mode |
| `:wq` | Save and quit |
| `:q!` | Quit without saving |
| `dd` | Delete the current line (in normal mode) |

---

## Man Pages — Built-in Help

Every command in Linux has a manual page. Learning to use `man` means you always have documentation available, even without internet access.

| Command | Description |
|--------|-------------|
| `man command` | Open the manual page for a command |
| `man -k keyword` | Search all man pages by keyword |
| `man 5 command` | Open a specific section of the manual |
| `/word` | Search for a word inside a man page |
| `n` | Jump to the next search match |
| `q` | Quit the man page |

### Man Page Sections
| Section | Contents |
|---------|----------|
| 1 | User commands |
| 5 | Configuration files |
| 8 | System administration commands |

---

## Examples

```bash
touch notes.txt
# Creates an empty file called notes.txt

echo "Hello World" > notes.txt
# Writes "Hello World" to notes.txt

echo "Second line" >> notes.txt
# Appends "Second line" to notes.txt

cat notes.txt
# Displays the contents of notes.txt

man ls
# Opens the manual for the ls command

man -k password
# Searches man pages for anything related to "password"
```

---

## Key Takeaway

`man` is your best friend — whenever you forget a command's options, look it up. Vim takes practice; focus on insert mode, Esc, `:wq`, and `:q!` first. Everything else in Vim can come later.
