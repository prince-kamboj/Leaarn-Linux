# Special Permissions in Linux

## Introduction

In addition to the standard **Read (r)**, **Write (w)**, and **Execute (x)** permissions, Linux provides three special permission bits that offer additional control over how files and directories behave.

These are:

- SUID (Set User ID)
- SGID (Set Group ID)
- Sticky Bit

These permissions are commonly used for:

- System Administration
- Shared Directories
- Security Management
- Privilege Escalation
- Ethical Hacking
- Penetration Testing

Understanding these permissions is essential because incorrect configuration can introduce serious security vulnerabilities.

---

# Standard Permissions Review

Every file has permissions for:

- Owner
- Group
- Others

Example

```bash
-rwxr-xr-x
```

Meaning

```
Owner  -> rwx
Group  -> r-x
Others -> r-x
```

Special permissions modify the behavior of these normal permissions.

---

# Types of Special Permissions

Linux provides three special permission bits.

| Permission | Numeric Value | Symbol |
|------------|--------------|--------|
| SUID | 4 | s |
| SGID | 2 | s |
| Sticky Bit | 1 | t |

---

# 1. SUID (Set User ID)

## What is SUID?

When a file has the **SUID** bit set, users execute the file with the permissions of the file's owner rather than their own.

Normally

```
Program

↓

Runs as current user
```

With SUID

```
Program

↓

Runs as file owner
```

---

## Example

```bash
ls -l /usr/bin/passwd
```

Output

```text
-rwsr-xr-x 1 root root ...
```

Notice

```
rws
```

The **s** replaces the owner's execute permission.

---

## Why Does passwd Need SUID?

A normal user cannot modify:

```text
/etc/shadow
```

However,

```bash
passwd
```

must update this file.

Because it has SUID, it temporarily runs with root privileges.

---

## Setting SUID

Symbolic

```bash
chmod u+s filename
```

Numeric

```bash
chmod 4755 filename
```

---

## Removing SUID

```bash
chmod u-s filename
```

Numeric

```bash
chmod 0755 filename
```

---

# 2. SGID (Set Group ID)

SGID behaves differently for files and directories.

---

## SGID on Files

When executed, the program runs with the file's group permissions.

Set SGID

```bash
chmod g+s filename
```

Numeric

```bash
chmod 2755 filename
```

---

## SGID on Directories

Files created inside the directory automatically inherit the directory's group.

Example

```
Projects/

├── file1
├── file2
```

All new files inherit

```
developers
```

instead of the creator's primary group.

This is useful for team collaboration.

---

## Example

Create directory

```bash
mkdir Project
```

Set SGID

```bash
chmod g+s Project
```

Check

```bash
ls -ld Project
```

Output

```text
drwxr-sr-x
```

---

# 3. Sticky Bit

Sticky Bit mainly applies to directories.

Without Sticky Bit

Users with write permission can delete any file in the directory.

With Sticky Bit

Only:

- File owner
- Directory owner
- Root

can delete a file.

---

## Example

The most common Sticky Bit directory is

```text
/tmp
```

Check

```bash
ls -ld /tmp
```

Output

```text
drwxrwxrwt
```

Notice

```
t
```

at the end.

---

## Setting Sticky Bit

Symbolic

```bash
chmod +t directory
```

Numeric

```bash
chmod 1777 directory
```

---

## Removing Sticky Bit

```bash
chmod -t directory
```

---

# Numeric Values

Special permissions use an additional digit before normal permissions.

| Number | Meaning |
|---------|---------|
| 4 | SUID |
| 2 | SGID |
| 1 | Sticky Bit |

Examples

```
4755
```

Owner has SUID.

```
2755
```

Group has SGID.

```
1777
```

Sticky Bit enabled.

```
6755
```

SUID + SGID.

```
7755
```

SUID + SGID + Sticky Bit.

---

# Reading Special Permissions

Example

```text
-rwsr-xr-x
```

Owner has SUID.

---

Example

```text
-rwxr-sr-x
```

Group has SGID.

---

Example

```text
drwxrwxrwt
```

Sticky Bit.

---

# Lowercase vs Uppercase

Sometimes you'll see uppercase letters.

```
S
```

Means SUID/SGID is set but execute permission is missing.

```
T
```

Means Sticky Bit is set but execute permission is missing.

Example

```
-rwSr--r--
```

---

# Finding Special Permission Files

Find all SUID files

```bash
find / -perm -4000 2>/dev/null
```

---

Find all SGID files

```bash
find / -perm -2000 2>/dev/null
```

---

Find Sticky Bit directories

```bash
find / -perm -1000 2>/dev/null
```

These commands are commonly used during Linux privilege escalation and security audits.

---

# Practical Examples

Enable SUID

```bash
chmod 4755 script
```

Enable SGID

```bash
chmod 2755 shared
```

Enable Sticky Bit

```bash
chmod 1777 uploads
```

Check

```bash
ls -l
```

---

# Cybersecurity Perspective

Special permissions are frequently exploited during privilege escalation.

Examples:

- Misconfigured SUID binaries
- Writable SUID executables
- Incorrect SGID configuration
- World-writable directories without Sticky Bit

During penetration testing, attackers often search for SUID files using:

```bash
find / -perm -4000 2>/dev/null
```

Security administrators should regularly audit these files.

---

# Common Mistakes

## Setting SUID on Scripts

Most modern Linux distributions ignore SUID on shell scripts for security reasons.

---

## Using Sticky Bit on Files

Sticky Bit is intended for directories, not regular files.

---

## Granting Unnecessary SUID Permissions

Giving SUID to custom programs can create privilege escalation vulnerabilities.

Only trusted system binaries should have SUID.

---

# Summary

Linux special permissions extend the standard permission model by providing additional control through **SUID**, **SGID**, and **Sticky Bit**. These permissions are widely used in system administration to enable controlled privilege escalation and collaborative directory management. Because they can introduce security risks if misconfigured, they are also a major focus during penetration testing and security audits.

---
