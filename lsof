# lsof — List Open Files

`lsof` (LiSt Open Files) lists which files are currently opened by which processes. Since Linux/Unix treats everything as a file (pipes, sockets, directories, devices, etc.), this command is invaluable for system diagnostics and troubleshooting.

---

## Understanding the Output

Running `lsof` without arguments lists all open files on the system. The output columns are:

| Column | Description |
|---|---|
| **COMMAND** | Process name |
| **PID** | Process ID |
| **USER** | Owner of the process |
| **FD** | File Descriptor (see below) |
| **TYPE** | File type (see below) |
| **DEVICE** | Device number |
| **SIZE/OFF** | File size or offset |
| **NODE** | Inode number |
| **NAME** | File path or name |

### File Descriptor (FD) Values

| Value | Meaning |
|---|---|
| `cwd` | Current working directory |
| `rtd` | Root directory |
| `txt` | Program text (code and data) |
| `mem` | Memory-mapped file |
| `<number>r` | Read access |
| `<number>w` | Write access |
| `<number>u` | Read and write access |

### TYPE Values

| Value | Meaning |
|---|---|
| `DIR` | Directory |
| `REG` | Regular file |
| `CHR` | Character special file |
| `FIFO` | First In First Out (pipe) |

---

## Common Commands

### List All Open Files

```bash
lsof
```

### Filter by User

List all files opened by a specific user:

```bash
lsof -u cyberpunk
```

Exclude a user with `^`:

```bash
lsof -i -u^root
```

### Find Processes on a Specific Port

```bash
lsof -i TCP:22
```

### List Processes on a Port Range

```bash
lsof -i TCP:1-1024
```

### Filter by IP Version

IPv4 only:

```bash
lsof -i 4
```

IPv6 only:

```bash
lsof -i 6
```

### List All Network Connections

Shows both LISTENING and ESTABLISHED connections:

```bash
lsof -i
```

### See What a User Is Doing

Combine `-i` with `-u` to see a user's network-related activity and open files:

```bash
lsof -i -u cyberpunk
```

### Search by PID

```bash
lsof -p 1
```

### Kill All Processes for a User

Uses `-t` (terse mode, outputs only PIDs) to feed into `kill`:

```bash
kill -9 $(lsof -t -u cyberpunk)
```

---

## Quick Reference

| Task | Command |
|---|---|
| All open files | `lsof` |
| Files by user | `lsof -u <user>` |
| Exclude a user | `lsof -i -u^<user>` |
| By port | `lsof -i TCP:<port>` |
| By port range | `lsof -i TCP:<start>-<end>` |
| IPv4 only | `lsof -i 4` |
| IPv6 only | `lsof -i 6` |
| All network connections | `lsof -i` |
| By PID | `lsof -p <pid>` |
| PIDs only (terse) | `lsof -t -u <user>` |
| Kill user processes | `kill -9 $(lsof -t -u <user>)` |

---

*Based on content from [NeverEndingSecurity](https://neverendingsecurity.wordpress.com/2015/04/13/lsof-commands-cheatsheet/).*
