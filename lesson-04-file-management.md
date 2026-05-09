# Lesson 4 — File Management

## Overview

Managing files and directories is something you will do constantly as a Linux administrator. This lesson also covers archiving and compression — essential skills for backups and transferring files.

## Directories

| Command | Description |
|--------|-------------|
| `mkdir dirname` | Create a new directory |
| `mkdir -p path/to/dir` | Create nested directories all at once |

## Copying & Moving

| Command | Description |
|--------|-------------|
| `cp file destination` | Copy a file |
| `cp -r dir destination` | Copy a directory and all its contents |
| `mv file destination` | Move or rename a file or directory |

## Deleting

| Command | Description |
|--------|-------------|
| `rm file` | Delete a file |
| `rm -r dir` | Delete a directory and all its contents |

> ⚠️ **Warning:** There is no trash bin on the command line. Deleted files are gone permanently. Always double-check before running `rm -r`.

## Links

| Command | Description |
|--------|-------------|
| `ln -s [target] [linkname]` | Create a soft (symbolic) link — like a shortcut |
| `ln [target] [linkname]` | Create a hard link — a direct reference to the same file data |

## Archives & Compression

### tar — Tape Archive

| Command | Description |
|--------|-------------|
| `tar -cvf archive.tar source` | Create a tar archive |
| `tar -xvf archive.tar` | Extract a tar archive |
| `tar -cvzf archive.tar.gz source` | Create a gzip compressed archive |
| `tar -cvjf archive.tar.bz2 source` | Create a bzip2 compressed archive |
| `tar -cvJf archive.tar.xz source` | Create an xz compressed archive |

**tar flags explained:**
- `c` — create
- `v` — verbose (show progress)
- `f` — file (specify the archive name)
- `x` — extract
- `z` — gzip compression
- `j` — bzip2 compression
- `J` — xz compression

### Individual Compression Tools

| Command | Description |
|--------|-------------|
| `gzip file` | Compress a file with gzip |
| `gzip -d file` | Decompress a gzip file |
| `bzip2 file` | Compress a file with bzip2 |
| `bzip2 -d file` | Decompress a bzip2 file |
| `xz file` | Compress a file with xz |
| `xz -d file` | Decompress an xz file |

## Examples

```bash
mkdir -p projects/rhcsa/notes
# Creates all three directories at once

cp notes.txt /tmp/
# Copies notes.txt to /tmp

mv notes.txt study-notes.txt
# Renames the file

rm -r old-project/
# Deletes the entire old-project directory

tar -cvzf backup.tar.gz /home/jason/
# Creates a compressed backup of the home directory

tar -xvf backup.tar.gz
# Extracts the archive in the current directory
```

---

## Key Takeaway

For the RHCSA, focus on `tar` with `-cvf` and `-xvf` as your core archive commands. Remember the compression flags: `z` for gzip, `j` for bzip2, `J` for xz. And always be careful with `rm -r`.
