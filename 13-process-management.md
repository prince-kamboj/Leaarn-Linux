# Process Management in Linux

## Introduction

A **process** is an instance of a running program. Every command, application, or service running on a Linux system executes as one or more processes.

Linux is a multitasking operating system, allowing multiple processes to run simultaneously. The operating system manages these processes by assigning CPU time, memory, priorities, and other system resources.

Understanding process management is essential for:

- Linux Administration
- DevOps
- System Monitoring
- Performance Tuning
- Ethical Hacking
- Penetration Testing
- Digital Forensics

---

# What is a Process?

A process is simply a program that is currently running.

Example:

```
Firefox

↓

Running Process
```

```
Python Script

↓

Running Process
```

```
SSH Server

↓

Background Process
```

Each process has its own:

- Process ID (PID)
- Parent Process ID (PPID)
- Owner
- Priority
- Memory allocation
- CPU usage
- Current state

---

# Process Lifecycle

A process generally moves through the following states:

```
New

↓

Ready

↓

Running

↓

Waiting

↓

Running

↓

Terminated
```

---

# Types of Processes

## Foreground Process

Runs directly in the terminal and requires user interaction.

Example

```bash
nano notes.txt
```

The terminal cannot be used until the program exits.

---

## Background Process

Runs independently of the terminal.

Example

```bash
firefox &
```

The `&` symbol starts the command in the background.

---

## Daemon Process

A daemon is a background service that starts automatically.

Examples:

- sshd
- cron
- systemd
- apache2
- nginx

---

# Viewing Running Processes

## ps Command

Displays currently running processes.

```bash
ps
```

Example

```text
PID TTY          TIME CMD
2451 pts/0    00:00:00 bash
2524 pts/0    00:00:00 ps
```

---

## ps -e

Display every running process.

```bash
ps -e
```

---

## ps -ef

Detailed process information.

```bash
ps -ef
```

Shows:

- User
- PID
- Parent PID
- CPU Time
- Command

---

## ps aux

One of the most commonly used commands.

```bash
ps aux
```

Displays:

- User
- PID
- CPU usage
- Memory usage
- Start time
- Running command

---

# Understanding ps aux Output

Example

```text
USER   PID %CPU %MEM COMMAND
root     1  0.1  0.2 systemd
```

| Column | Description |
|----------|------------|
| USER | Process owner |
| PID | Process ID |
| %CPU | CPU usage |
| %MEM | Memory usage |
| COMMAND | Executed program |

---

# Process ID (PID)

Every process has a unique Process ID.

View current shell PID

```bash
echo $$
```

Example

```text
3245
```

---

# Parent Process ID (PPID)

Each process is created by another process.

View parent process

```bash
ps -o ppid= -p $$
```

---

# top Command

Displays live system activity.

```bash
top
```

Shows

- Running processes
- CPU usage
- Memory usage
- Load average
- Uptime

Exit

```
q
```

---

# htop Command

A more user-friendly version of `top`.

Install

Ubuntu/Debian

```bash
sudo apt install htop
```

Run

```bash
htop
```

Advantages

- Colorful interface
- Mouse support
- Easy sorting
- Search functionality

Exit

```
F10
```

---

# Finding Processes

Search for a process

```bash
ps aux | grep firefox
```

Example

```bash
ps aux | grep ssh
```

---

# pgrep

Find PID by process name.

```bash
pgrep firefox
```

---

# pidof

Returns the PID of a program.

```bash
pidof sshd
```

---

# Killing Processes

Terminate a process

```bash
kill PID
```

Example

```bash
kill 4521
```

---

# Force Kill

```bash
kill -9 PID
```

Example

```bash
kill -9 4521
```

Use only if a process refuses to stop.

---

# killall

Kill by program name.

```bash
killall firefox
```

---

# pkill

Kill using the process name.

```bash
pkill firefox
```

---

# Background Jobs

Start background process

```bash
sleep 100 &
```

View jobs

```bash
jobs
```

Output

```text
[1]+ Running sleep 100 &
```

---

# Bringing Jobs to Foreground

```bash
fg
```

Specific job

```bash
fg %1
```

---

# Sending to Background

Suspend

```
Ctrl + Z
```

Resume in background

```bash
bg
```

---

# nohup

Keeps a process running after logout.

```bash
nohup python app.py &
```

Output is saved to

```
nohup.out
```

---

# Process Priority

Linux schedules processes using priorities.

Lower value

↓

Higher priority

---

# nice

Start a process with custom priority.

```bash
nice -n 10 python script.py
```

Default priority

```
0
```

Range

```
-20

↓

19
```

-20 = Highest priority

19 = Lowest priority

---

# renice

Change priority of a running process.

```bash
sudo renice -5 -p 1234
```

---

# Process Tree

View parent-child relationships.

```bash
pstree
```

Install if missing

```bash
sudo apt install psmisc
```

---

# System Monitor

Modern Linux distributions include graphical tools like:

- GNOME System Monitor
- KDE System Monitor

These display CPU, memory, network, and running processes.

---

# Practical Examples

Display all processes

```bash
ps aux
```

Find SSH process

```bash
ps aux | grep ssh
```

Monitor processes

```bash
top
```

Kill Firefox

```bash
killall firefox
```

Run Python in background

```bash
python app.py &
```

Resume stopped process

```bash
bg
```

Bring process back

```bash
fg
```

---

# Common Mistakes

## Killing the Wrong Process

Always verify the PID before using:

```bash
kill -9
```

---

## Using kill -9 Immediately

Try

```bash
kill PID
```

first.

Use

```bash
kill -9 PID
```

only if necessary.

---

## Forgetting nohup

Programs started remotely may stop after logout.

Use

```bash
nohup command &
```

---

# Cybersecurity Perspective

Process management is critical during security investigations.

Security analysts use it to:

- Detect malicious processes
- Monitor suspicious applications
- Identify crypto miners
- Find reverse shells
- Kill unauthorized programs

Common commands:

```bash
ps aux
```

```bash
top
```

```bash
pgrep
```

```bash
kill
```

```bash
pstree
```

These commands are frequently used in CTFs, incident response, malware analysis, and penetration testing.

---

# Summary

Process management is the practice of monitoring, controlling, and terminating running programs in Linux. Tools such as `ps`, `top`, `htop`, `kill`, `killall`, `pgrep`, `jobs`, `bg`, `fg`, and `nohup` help administrators and security professionals manage system activity efficiently. Mastering these commands is essential for troubleshooting, performance tuning, and cybersecurity.

---

