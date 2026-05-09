# Lesson 2 Lab — Solutions


1. Create an empty file called `testfile.txt`.
```bash
touch testfile.txt
```

2. Write "Hello RHCSA" into `notes.txt`.
```bash
echo "Hello RHCSA" > notes.txt
```

3. Append "Study hard" to `notes.txt`.
```bash
echo "Study hard" >> notes.txt
```

4. Display contents of `notes.txt`.
```bash
cat notes.txt
```

5. Open `notes.txt` in Vim, add a line, save and quit.
```bash
vim notes.txt
# Press i to enter insert mode
# Navigate to end, add new line: Exam ready
# Press Esc, then type :wq and press Enter
```

6. Open man page for `ls` and find `-h`.
```bash
man ls
# Inside man page, type /\-h and press Enter to search
# Press q to quit
```

7. Search man pages for "password".
```bash
man -k password
```

8. Open section 5 of the `passwd` man page.
```bash
man 5 passwd
```
