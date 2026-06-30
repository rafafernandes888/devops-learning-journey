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

## 01.3 — Linux services

A service is a process that usually runs in the background and provides functionality to the system or to an application.

Examples of services:

- `cron` — runs scheduled tasks
- `rsyslog` — stores system logs
- `systemd-journald` — manages system journal logs
- `systemd-resolved` — handles DNS name resolution
- `ssh` — allows remote access
- `docker` — runs containers

A process is any program currently running.

A service is usually a long-running background process managed by the system.

In simple terms:

```text
Every service is a process, but not every process is a service.
```

### Useful service commands

| Command | Purpose |
|---|---|
| `systemctl --version` | Shows the installed systemd version |
| `systemctl is-system-running` | Shows the general system state |
| `systemctl list-units --type=service --state=running --no-pager` | Lists running services |
| `systemctl status cron --no-pager` | Shows detailed status for the cron service |
| `systemctl is-active cron` | Shows if cron is currently running |
| `systemctl is-enabled cron` | Shows if cron starts automatically on boot |
| `systemctl --failed` | Shows failed services |
| `sudo systemctl restart cron` | Restarts the cron service |

### Reading service status

When checking a service with:

```bash
systemctl status cron --no-pager
```

Important fields include:

| Field | Meaning |
|---|---|
| `Loaded` | Shows if the service unit was loaded correctly |
| `Active` | Shows if the service is running, stopped or failed |
| `Main PID` | Shows the main process ID of the service |
| `Memory` | Shows memory usage |
| `CPU` | Shows CPU usage |
| Recent logs | Show recent events related to the service |

### cron

`cron` is a Linux service used to run scheduled tasks automatically.

Examples:

- Backups
- Maintenance scripts
- Hourly or daily tasks
- Startup tasks

### rsyslog

`rsyslog` is a Linux service used to collect and store system log messages.

Common log files:

```text
/var/log/syslog
/var/log/auth.log
/var/log/kern.log
```

Example commands:

```bash
sudo tail -n 20 /var/log/syslog
grep CRON /var/log/syslog | tail -n 10
```

In simple terms:

```text
cron runs scheduled tasks.
rsyslog records what happened in the system.
```

---

## 01.4 — Linux networking commands

Linux networking commands are useful to diagnose connectivity, DNS, HTTP responses and open ports.

### Useful networking commands

| Command | Purpose |
|---|---|
| `ip addr` | Shows network interfaces and IP addresses |
| `ping -c 4 google.com` | Tests connectivity to a host |
| `curl -I https://example.com` | Shows HTTP/HTTPS response headers |
| `ss -tuln` | Shows listening TCP/UDP ports |
| `resolvectl query google.com` | Tests DNS name resolution |

### Important concepts

| Concept | Meaning |
|---|---|
| IP address | Identifies a machine in a network |
| DNS | Translates domain names into IP addresses |
| Port | Identifies a specific service on a machine |
| HTTP | Web protocol without encryption |
| HTTPS | Web protocol with encryption |
| localhost | Refers to the local machine |

### Examples from practice

```bash
ip addr
```

This shows interfaces such as `lo` and `eth0`.

`lo` is the loopback interface and usually uses:

```text
127.0.0.1
```

`eth0` is usually the main network interface.

```bash
ping -c 4 google.com
```

If packets are transmitted and received with `0% packet loss`, connectivity is working.

```bash
curl -I https://example.com
```

A response such as:

```text
HTTP/2 200
```

means the website responded successfully.

```bash
ss -tuln
```

This shows listening ports. Port `53` is commonly used for DNS.

```bash
resolvectl query google.com
```

This checks if DNS can translate a domain name into IP addresses.

---

## 01.5 — System logs

To be completed.
