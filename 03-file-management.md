# Linux File Management

## Introduction

Linux provides powerful commands for creating, copying, moving, renaming, deleting, and managing files and directories. Understanding these commands is essential for system administration, scripting, and cybersecurity tasks.

---

# Creating Files

## `touch`

Creates a new empty file or updates the timestamp of an existing file.

### Syntax

```bash
touch filename
```

### Example

```bash
touch notes.txt
```

Create multiple files:

```bash
touch file1.txt file2.txt file3.txt
```

---

# Creating Directories

## `mkdir`

Creates a new directory.

### Syntax

```bash
mkdir directory_name
```

### Example

```bash
mkdir Documents
```

Create multiple directories:

```bash
mkdir Linux Python Networking
```

Create nested directories:

```bash
mkdir -p Projects/Linux/Basics
```

---

# Listing Files

## `ls`

Displays files and directories.

```bash
ls
```

Long listing:

```bash
ls -l
```

Show hidden files:

```bash
ls -la
```

---

# Copying Files

## `cp`

Copies files and directories.

### Syntax

```bash
cp source destination
```

### Example

```bash
cp notes.txt backup.txt
```

Copy a file to another directory:

```bash
cp notes.txt Documents/
```

Copy multiple files:

```bash
cp file1.txt file2.txt Backup/
```

Copy directories recursively:

```bash
cp -r Projects Backup/
```

---

# Moving and Renaming Files

## `mv`

Moves or renames files and directories.

### Move a file

```bash
mv notes.txt Documents/
```

### Rename a file

```bash
mv oldname.txt newname.txt
```

### Rename a directory

```bash
mv LinuxNotes Linux_Notes
```

---

# Removing Files

## `rm`

Deletes files.

### Delete a file

```bash
rm notes.txt
```

Delete multiple files:

```bash
rm file1.txt file2.txt
```

Ask before deleting:

```bash
rm -i notes.txt
```

Force delete:

```bash
rm -f notes.txt
```

---

# Removing Directories

## `rmdir`

Deletes an empty directory.

```bash
rmdir Test
```

---

## Delete Non-Empty Directories

```bash
rm -r Projects
```

Force delete recursively:

```bash
rm -rf Projects
```

> ⚠️ **Warning:** `rm -rf` permanently deletes files and directories without moving them to a recycle bin. Always double-check the path before using it.

---

# Viewing File Contents

## `cat`

Displays the contents of a file.

```bash
cat notes.txt
```

Display multiple files:

```bash
cat file1.txt file2.txt
```

Create a file with `cat`:

```bash
cat > notes.txt
```

Finish input with:

```text
Ctrl + D
```

---

# Viewing Large Files

## `less`

Allows scrolling through a file.

```bash
less logfile.txt
```

Useful shortcuts:

- `Space` → Next page
- `b` → Previous page
- `q` → Quit

---

## `more`

Displays one page at a time.

```bash
more logfile.txt
```

---

# First and Last Lines

## `head`

Shows the first 10 lines.

```bash
head notes.txt
```

First 5 lines:

```bash
head -5 notes.txt
```

---

## `tail`

Shows the last 10 lines.

```bash
tail notes.txt
```

Last 20 lines:

```bash
tail -20 notes.txt
```

Monitor a log file in real time:

```bash
tail -f /var/log/syslog
```

---

# Counting File Information

## `wc`

Counts lines, words, and characters.

```bash
wc notes.txt
```

Only lines:

```bash
wc -l notes.txt
```

Only words:

```bash
wc -w notes.txt
```

Only characters:

```bash
wc -m notes.txt
```

---

# File Information

## `file`

Displays the file type.

```bash
file notes.txt
```

Example output:

```text
notes.txt: ASCII text
```

---

# Locate a Command

## `which`

Shows the location of an executable.

```bash
which python3
```

Output:

```text
/usr/bin/python3
```

---

# Search for Files

## `find`

Find a file by name.

```bash
find . -name notes.txt
```

Find all `.txt` files:

```bash
find . -name "*.txt"
```

---

# Searching Inside Files

## `grep`

Searches for text inside files.

```bash
grep "Linux" notes.txt
```

Ignore case:

```bash
grep -i "linux" notes.txt
```

Search recursively:

```bash
grep -r "password" .
```

---

# Wildcards

## `*`

Matches any number of characters.

```bash
ls *.txt
```

---

## `?`

Matches a single character.

```bash
ls file?.txt
```

---

# Absolute vs Relative Paths

Absolute path:

```text
/home/prince/Documents/notes.txt
```

Relative path:

```text
Documents/notes.txt
```

---

# File Permissions Preview

Display permissions:

```bash
ls -l
```

Example:

```text
-rw-r--r-- 1 prince prince 120 notes.txt
```


---

# Common File Management Workflow

```bash
mkdir Linux
cd Linux

touch notes.txt

cp notes.txt backup.txt

mv backup.txt backup_notes.txt

cat notes.txt

rm backup_notes.txt

cd ..

rmdir Linux
```

---



# Summary

| Command | Purpose |
|---------|---------|
| `touch` | Create a file |
| `mkdir` | Create a directory |
| `ls` | List files and directories |
| `cp` | Copy files or directories |
| `mv` | Move or rename files |
| `rm` | Delete files |
| `rmdir` | Delete empty directories |
| `cat` | Display file contents |
| `less` | View large files |
| `head` | Show beginning of a file |
| `tail` | Show end of a file |
| `wc` | Count lines, words, and characters |
| `file` | Identify file type |
| `find` | Search for files |
| `grep` | Search text inside files |

---

