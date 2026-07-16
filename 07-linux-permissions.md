# Linux File Permissions

## Introduction

Linux is a multi-user operating system where multiple users can access the same system. To protect files and directories from unauthorized access, Linux uses a permission system.

Every file and directory has a set of permissions that determine:

- Who can read the file
- Who can modify the file
- Who can execute the file
- Who owns the file
- Which group can access the file

Understanding Linux permissions is essential for:

- Linux Administration
- Shell Scripting
- Server Management
- DevOps
- Ethical Hacking
- Penetration Testing

---

# Why Are Permissions Important?

Permissions help:

- Protect sensitive data
- Prevent accidental deletion
- Restrict unauthorized access
- Secure system files
- Control user access

Example

```
/etc/shadow
```

contains password hashes and should only be accessible by the root user.

---

# Ownership in Linux

Every file has three ownership attributes.

| Ownership | Description |
|-----------|-------------|
| User (Owner) | Person who owns the file |
| Group | Group associated with the file |
| Others | Everyone else |

Example

```bash
-rw-r--r-- 1 prince users 1500 Jul 10 notes.txt
```

Here:

- Owner → prince
- Group → users
- Others → Everyone else

---

# Viewing Permissions

Use:

```bash
ls -l
```

Example

```bash
-rwxr-xr-- 1 prince users 500 script.sh
```

---

# Understanding Permission Format

```
-rwxr-xr--
```

Breakdown

```
-

rwx

r-x

r--
```

First Character

| Symbol | Meaning |
|---------|---------|
| - | File |
| d | Directory |
| l | Symbolic Link |
| c | Character Device |
| b | Block Device |

---

Owner Permissions

```
rwx
```

Group Permissions

```
r-x
```

Others Permissions

```
r--
```

---

# Permission Types

There are three basic permissions.

| Symbol | Value | Meaning |
|---------|-------|---------|
| r | 4 | Read |
| w | 2 | Write |
| x | 1 | Execute |

---

# Read Permission (r)

Allows:

- View file contents
- Open a file

Example

```bash
cat notes.txt
```

Without read permission:

```
Permission denied
```

---

# Write Permission (w)

Allows:

- Modify file
- Edit file
- Delete file (directory permissions also apply)

Example

```bash
echo "Linux" >> notes.txt
```

---

# Execute Permission (x)

Allows running executable files or scripts.

Example

```bash
./script.sh
```

Without execute permission:

```
Permission denied
```

---

# Permission Values

Permissions are represented using binary values.

| Permission | Value |
|------------|------|
| Read | 4 |
| Write | 2 |
| Execute | 1 |

Examples

```
7 = 4+2+1 = rwx

6 = 4+2 = rw-

5 = 4+1 = r-x

4 = r--

3 = -wx

2 = -w-

1 = --x

0 = ---
```

---

# Numeric Permission Table

| Number | Permission |
|---------|------------|
| 7 | rwx |
| 6 | rw- |
| 5 | r-x |
| 4 | r-- |
| 3 | -wx |
| 2 | -w- |
| 1 | --x |
| 0 | --- |

---

# Common Permission Modes

755

```
rwx r-x r-x
```

Used for

- Directories
- Executable programs

---

644

```
rw- r-- r--
```

Used for

- Text files
- Configuration files

---

700

```
rwx ---
---
```

Only owner has access.

---

600

```
rw-
---
---
```

Used for

- SSH private keys
- Password files

---

777

```
rwx rwx rwx
```

Everyone has full access.

⚠ Never use this unless absolutely necessary.

---

# Changing Permissions

Use:

```bash
chmod
```

Syntax

```bash
chmod permissions filename
```

---

# Numeric Method

Example

```bash
chmod 755 script.sh
```

Permissions become

```
rwxr-xr-x
```

---

Example

```bash
chmod 644 notes.txt
```

---

# Symbolic Method

Add Execute Permission

```bash
chmod +x script.sh
```

Remove Execute

```bash
chmod -x script.sh
```

---

Add Write Permission

```bash
chmod +w notes.txt
```

---

Remove Write Permission

```bash
chmod -w notes.txt
```

---

Give Owner Execute

```bash
chmod u+x script.sh
```

---

Give Group Write

```bash
chmod g+w project.txt
```

---

Remove Others Read

```bash
chmod o-r file.txt
```

---

# User Symbols

| Symbol | Meaning |
|---------|---------|
| u | User |
| g | Group |
| o | Others |
| a | All |

Example

```bash
chmod a+x script.sh
```

Everyone gets execute permission.

---

# Changing Ownership

Owner

```bash
sudo chown prince file.txt
```

Owner and Group

```bash
sudo chown prince:developers file.txt
```

---

# Change Group

```bash
sudo chgrp developers file.txt
```

---

# Directory Permissions

Directories use the same permissions but with different meanings.

Read

Allows listing files.

```bash
ls directory
```

Write

Allows creating or deleting files.

Execute

Allows entering the directory.

```bash
cd directory
```

---

# Special Permissions

Linux provides three special permission bits.

## SUID

Runs executable as file owner.

Example

```bash
passwd
```

---

## SGID

Files inherit group ownership.

Useful for shared project folders.

---

## Sticky Bit

Only file owner can delete files.

Common example

```
/tmp
```

Permissions

```
drwxrwxrwt
```

---

# Checking Permissions

```bash
ls -l
```

Check directory

```bash
ls -ld Downloads
```

---

# Practical Examples

Make a script executable

```bash
chmod +x backup.sh
```

---

Private SSH Key

```bash
chmod 600 id_rsa
```

---

Public Key

```bash
chmod 644 id_rsa.pub
```

---

Secure Directory

```bash
chmod 700 secret
```

---

# Common Mistakes

Using 777

```bash
chmod 777 file.txt
```

Avoid unless necessary.

---

Forgetting Execute Permission

```bash
./script.sh
```

Error

```
Permission denied
```

Fix

```bash
chmod +x script.sh
```

---

Editing System Files Without sudo

```bash
nano /etc/hosts
```

May fail.

Use

```bash
sudo nano /etc/hosts
```

---



# Summary

Linux permissions control who can read, write, and execute files and directories. Understanding ownership, permission bits, `chmod`, `chown`, and `chgrp` is essential for maintaining secure Linux systems. Proper permission management helps protect sensitive data and prevents unauthorized access.

---

