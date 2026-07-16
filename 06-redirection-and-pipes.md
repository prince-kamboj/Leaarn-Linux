# Input/Output Redirection and Pipes in Linux

## Introduction

Linux commands communicate using three standard data streams:

- **Standard Input (stdin)** – Receives input from the keyboard or another command.
- **Standard Output (stdout)** – Displays normal command output.
- **Standard Error (stderr)** – Displays error messages.

Redirection allows you to change where these streams read from or write to. Pipes allow the output of one command to become the input of another command.

These concepts are fundamental to Linux and are heavily used in scripting, automation, system administration, and cybersecurity.

---

# Standard Streams

Every Linux command uses three standard streams.

| Stream | File Descriptor | Description |
|---------|----------------|-------------|
| Standard Input | 0 | Input to a command |
| Standard Output | 1 | Normal output |
| Standard Error | 2 | Error messages |

Example

```bash
cat
```

Type:

```text
Hello Linux
```

Output

```text
Hello Linux
```

Press

```text
Ctrl + D
```

to stop.

---

# Output Redirection (>)

The `>` operator redirects the output of a command to a file.

If the file does not exist, it is created.

If the file already exists, its contents are overwritten.

## Syntax

```bash
command > filename
```

Example

```bash
ls > files.txt
```

Instead of displaying the output on the terminal, it is stored in `files.txt`.

---

## View the File

```bash
cat files.txt
```

---

# Append Output (>>)

The `>>` operator appends output to the end of a file.

It does not overwrite existing content.

## Syntax

```bash
command >> filename
```

Example

```bash
date >> log.txt
```

Running the command multiple times will add a new line each time.

---

# Difference Between > and >>

| Operator | Action |
|-----------|--------|
| `>` | Overwrites existing file |
| `>>` | Appends to existing file |

Example

```bash
echo "First Line" > notes.txt
```

```bash
echo "Second Line" >> notes.txt
```

Output

```text
First Line
Second Line
```

---

# Input Redirection (<)

The `<` operator sends a file as input to a command.

## Syntax

```bash
command < filename
```

Example

```bash
sort < names.txt
```

Instead of typing the names manually, `sort` reads them from the file.

---

# Standard Error Redirection (2>)

Redirects only error messages.

## Syntax

```bash
command 2> error.txt
```

Example

```bash
ls unknownfile 2> errors.txt
```

The error message is stored in `errors.txt`.

---

# Append Error Messages (2>>)

```bash
command 2>> errors.txt
```

Adds new errors to the existing file.

---

# Redirect Both Output and Errors

Store both normal output and errors.

```bash
command > output.txt 2>&1
```

Example

```bash
ls file1 missingfile > result.txt 2>&1
```

---

# Discard Output

Linux provides a special device:

```text
/dev/null
```

Anything sent here is discarded.

Hide normal output

```bash
command > /dev/null
```

Hide error messages

```bash
command 2> /dev/null
```

Hide everything

```bash
command > /dev/null 2>&1
```

---

# Pipes (|)

A pipe sends the output of one command directly to another command.

## Syntax

```bash
command1 | command2
```

Instead of saving output to a file, it is immediately processed by the next command.

---

## Example 1

```bash
ls | sort
```

Output

The list of files is sorted alphabetically.

---

## Example 2

```bash
cat names.txt | sort
```

Sorts the contents of the file.

---

## Example 3

```bash
cat users.txt | grep "root"
```

Displays only lines containing "root".

---

## Example 4

```bash
cat users.txt | wc -l
```

Counts the number of lines.

---

## Multiple Pipes

Commands can be chained together.

```bash
cat users.txt | sort | uniq
```

Process:

```
File

↓

Sort

↓

Remove duplicates
```

---

Another example

```bash
ps aux | grep firefox
```

Displays only Firefox-related processes.

---

# tee Command

Normally, a pipe passes output to another command.

The `tee` command allows you to display the output **and** save it to a file at the same time.

Example

```bash
ls | tee files.txt
```

The output appears on the terminal and is also saved in `files.txt`.

Append

```bash
ls | tee -a files.txt
```

---

# xargs with Pipes

`xargs` converts input into command arguments.

Example

```bash
find . -name "*.txt" | xargs rm
```

Deletes every `.txt` file found.

> **Warning:** Be careful when combining `xargs` with commands like `rm`, as it can permanently delete files.

---

# Real-World Examples

## Search Running SSH Processes

```bash
ps aux | grep ssh
```

---

## Count Log Entries

```bash
cat access.log | wc -l
```

---

## Find Failed Login Attempts

```bash
grep "Failed password" /var/log/auth.log
```

---

## Display Top 10 Processes

```bash
ps aux | head
```

---

## View Last 20 Log Entries

```bash
tail -20 /var/log/syslog
```

---

## Find Python Files

```bash
find . -name "*.py"
```

---

## Count Python Files

```bash
find . -name "*.py" | wc -l
```

---

## Save Directory Listing

```bash
ls -la > directory.txt
```

---

## Save Errors Only

```bash
find /root 2> errors.txt
```

---

# Common Mistakes

### Accidentally Overwriting Files

Incorrect

```bash
ls > notes.txt
```

This removes existing content.

Use

```bash
ls >> notes.txt
```

if you want to keep previous data.

---

### Forgetting Quotes

Incorrect

```bash
grep Failed password logfile
```

Correct

```bash
grep "Failed password" logfile
```

---

### Ignoring Error Messages

Sometimes errors are useful for troubleshooting.

Avoid redirecting errors to `/dev/null` unless you intentionally want to suppress them.

---


# Summary

Input/output redirection and pipes are powerful Linux features that allow commands to work together efficiently. Redirection controls where input, output, and errors are sent, while pipes connect multiple commands into a single workflow. Mastering these concepts is essential for Linux administration, shell scripting, automation, and cybersecurity.

---

