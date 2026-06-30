# Linux Fundamentals

## What is Linux?

Linux is an operating system widely used in servers, cloud environments, containers and DevOps workflows.

As a future DevOps engineer, Linux is important because many production systems run on Linux servers.

## Basic Commands

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
| `ps` | Shows running processes |
| `top` | Shows system resource usage |

## Practice

Today I practiced creating folders and files and navigating through directories.

## Searching logs with grep

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
| `grep -E "ERROR|WARN" app.log` | Shows lines containing ERROR or WARN |

Example:

```bash
grep -n ERROR app.log