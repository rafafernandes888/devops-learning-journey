# Linux Fundamentals

## What is Linux?

Linux is an operating system widely used in servers, cloud environments, containers and DevOps workflows.

As a future DevOps engineer, Linux is important because many production systems run on Linux servers.

---

## 01.1 — Files, logs, grep, permissions and scripts

### Basic commands

| Command | Purpose |
|---|---|
| `pwd` | Shows the current directory |
| `ls` | Lists files and folders |
| `cd` | Changes directory |
| `mkdir` | Creates a folder |
| `touch` | Creates an empty file |
| `cp` | Copies files or folders |
| `mv` | Moves or renames files or folders |
| `rm` | Removes files or folders |
| `cat` | Shows file content |
| `grep` | Searches text inside files |
| `chmod` | Changes file permissions |

### Practice

Today I practiced creating folders and files, navigating through directories, reading files, filtering logs and working with Linux permissions.

### Searching logs with grep

In Linux, logs are used to understand what is happening inside an application or system.

Common log levels:

| Level | Meaning |
|---|---|
| INFO | Normal information |
| WARN | Warning that may become a problem |
| ERROR | Something failed |
| DEBUG | Technical details for investigation |

Useful commands:

| Command | Purpose |
|---|---|
| `cat app.log` | Shows the full log file |
| `grep ERROR app.log` | Shows only lines containing ERROR |
| `grep -n ERROR app.log` | Shows ERROR lines with line numbers |
| `grep -E "ERROR\|WARN" app.log` | Shows lines containing ERROR or WARN |

Example:

```bash
grep -n ERROR app.log
```

This helps quickly find where problems happened in a log file.

### Reading parts of log files

Large log files can have thousands of lines. Instead of using `cat` to show everything, we can use `head` and `tail`.

| Command | Purpose |
|---|---|
| `head app.log` | Shows the first 10 lines |
| `head -n 2 app.log` | Shows the first 2 lines |
| `tail app.log` | Shows the last 10 lines |
| `tail -n 2 app.log` | Shows the last 2 lines |

`tail` is useful because recent errors usually appear at the end of log files.

### Following logs in real time

`tail -f` is used to follow a log file in real time.

Example:

```bash
tail -f app.log
```

This shows the last lines of the file and keeps waiting for new lines.

To stop it:

```text
Ctrl + C
```

This is useful in DevOps when checking application logs while the system is running.

### File permissions

Linux files and directories have permissions for three groups:

| Group | Meaning |
|---|---|
| User / owner | The owner of the file |
| Group | Users in the file's group |
| Others | Everyone else |

Permission values:

| Permission | Value | Meaning |
|---|---|---|
| `r` | 4 | Read |
| `w` | 2 | Write |
| `x` | 1 | Execute |

Example:

```text
-rwxr--r--
```

This means:

| Group | Permissions |
|---|---|
| Owner | Read, write and execute |
| Group | Read only |
| Others | Read only |

### chmod

`chmod` is used to change file permissions.

Examples:

```bash
chmod +x deploy.sh
```

Adds execute permission.

```bash
chmod 744 deploy.sh
```

Sets permissions to:

```text
owner: rwx
group: r--
others: r--
```

This is useful for scripts that should only be executed by the owner.

### Shell scripts

A shell script can start with:

```bash
#!/bin/bash
```

This tells Linux to run the script using Bash.

Example:

```bash
#!/bin/bash
echo "Deploy started"
```

To execute the script:

```bash
./deploy.sh
```

---

## 01.2 — Linux processes

A process is a program that is currently running.

Examples of processes:

- Terminal sessions
- Linux commands
- Shell scripts
- System services
- Applications

Each process has a PID, which means Process ID.

### Useful process commands

| Command | Purpose |
|---|---|
| `ps` | Shows processes from the current terminal |
| `ps aux` | Shows processes from the whole system |
| `ps aux \| grep bash` | Searches for processes containing `bash` |
| `sleep 300 &` | Starts a process in the background |
| `kill PID` | Terminates a process by its PID |
| `top` | Shows processes in real time |

### Example

```bash
sleep 300 &
ps aux | grep sleep
kill 10233
```

In this example, `sleep 300` creates a process, `ps aux | grep sleep` finds it, and `kill` terminates it using its PID.

`ps` shows a snapshot of processes at one moment.

`top` shows processes in real time and updates automatically.

---


