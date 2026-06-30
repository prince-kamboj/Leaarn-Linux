# Linux Navigation Commands

Navigation commands are used to move around the Linux filesystem and identify your current location.

---

# 1. pwd

Displays the current working directory.

## Syntax

```bash
pwd
```

## Example

```bash
$ pwd
/home/prince
```

## Use Case

Useful when you are unsure about your current location in the filesystem.

---

# 2. ls

Lists files and directories in the current location.

## Syntax

```bash
ls
```

## Example

```bash
$ ls
Documents Downloads Pictures Videos
```

---

# 3. ls -l

Displays files in long listing format.

## Syntax

```bash
ls -l
```

## Example

```bash
drwxr-xr-x 2 prince prince 4096 Jun 30 Documents
-rw-r--r-- 1 prince prince  512 Jun 30 notes.txt
```

## Shows

- File permissions
- Owner
- Group
- Size
- Modification date

---

# 4. ls -a

Displays all files including hidden files.

## Syntax

```bash
ls -a
```

## Example

```bash
$ ls -a
.  ..  .bashrc  .profile  Documents
```

Files beginning with `.` are hidden files.

---

# 5. ls -la

Combines long listing and hidden files.

## Syntax

```bash
ls -la
```

## Example

```bash
$ ls -la
drwxr-xr-x 4 prince prince 4096 Jun 30 .
drwxr-xr-x 3 root   root   4096 Jun 30 ..
-rw-r--r-- 1 prince prince  220 Jun 30 .bashrc
```

---

# 6. cd

Changes the current directory.

## Syntax

```bash
cd directory_name
```

## Example

```bash
cd Documents
```

---

# 7. cd ..

Moves one directory up.

## Example

```bash
cd ..
```

Example:

```text
/home/prince/Documents
        ↓
/home/prince
```

---

# 8. cd ~

Moves directly to the user's home directory.

## Example

```bash
cd ~
```

Output location:

```text
/home/prince
```

---

# 9. cd /

Moves to the root directory.

## Example

```bash
cd /
```

Root directory:

```text
/
```

---

# 10. cd -

Returns to the previous directory.

## Example

```bash
cd -
```

Example:

```text
/home/prince/Documents
↓
/etc
↓
cd -
↓
/home/prince/Documents
```

---

# 11. tree

Displays directories in a tree structure.

## Syntax

```bash
tree
```

## Example

```text
.
├── Documents
├── Downloads
└── Pictures
```

If not installed:

```bash
sudo apt install tree
```

---

# 12. find

Searches for files and directories.

## Syntax

```bash
find [path] [options]
```

## Example

```bash
find . -name notes.txt
```

Searches for:

```text
notes.txt
```

inside the current directory.

---

# 13. locate

Quickly searches for files using a database.

## Syntax

```bash
locate filename
```

## Example

```bash
locate passwd
```

If database is outdated:

```bash
sudo updatedb
```

---

# 14. which

Shows the location of executable commands.

## Example

```bash
which python3
```

Output:

```text
/usr/bin/python3
```

---

# 15. whereis

Displays binary, source and manual page locations.

## Example

```bash
whereis bash
```

Output:

```text
bash: /usr/bin/bash /usr/share/man/man1/bash.1.gz
```

---

# 16. realpath

Displays the absolute path of a file or directory.

## Example

```bash
realpath notes.txt
```

Output:

```text
/home/prince/Documents/notes.txt
```

---

# 17. dirname

Displays the parent directory of a path.

## Example

```bash
dirname /home/prince/Documents/notes.txt
```

Output:

```text
/ home/prince/Documents
```

---

# 18. basename

Displays only the filename.

## Example

```bash
basename /home/prince/Documents/notes.txt
```

Output:

```text
notes.txt
```

---

# 19. pushd

Saves the current directory and moves to another.

## Example

```bash
pushd /etc
```

---

# 20. popd

Returns to the directory saved using pushd.

## Example

```bash
popd
```

---

# Common Navigation Workflow

```bash
pwd
ls -la
cd Documents
pwd
cd ..
cd ~
```

---

# Filesystem Hierarchy

```text
/
├── bin
├── boot
├── dev
├── etc
├── home
│   └── prince
├── lib
├── opt
├── proc
├── root
├── tmp
├── usr
└── var
```

---

# Key Takeaways

- `pwd` shows current location.
- `ls` lists files and directories.
- `cd` changes directories.
- `tree` visualizes directory structure.
- `find` and `locate` search for files.
- `which` and `whereis` locate executables.
- Understanding filesystem navigation is essential for Linux administration and cybersecurity work.