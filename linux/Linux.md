# 📚 Linux.md - CyberBible Cisco Internship

---

## 🧠 Basic Commands

Linux commands are programs created to perform a specific task. Use the `man` command (short for manual) to obtain documentation about commands. As an example:

```bash
man ls
```

Because commands are programs stored on the disk, when a user types a command, the shell must find it on the disk before it can be executed. The shell will look for user-typed commands in specific directories and attempt to execute them. The list of directories checked by the shell is called the path. The path contains many directories commonly used to store commands. If a command is not in the path, the user must specify its location, or the shell will not be able to find it. Users can easily add directories to the path, if necessary.

To invoke a command via the shell, simply type its name. The shell will try to find it in the system path and execute it.

### 🔧 Basic Linux Commands

| Command   | Description                                                                 |
|-----------|-----------------------------------------------------------------------------|
| `mv`      | Moves or renames files and directories                                      |
| `chmod`   | Modifies file permissions                                                   |
| `chown`   | Changes the ownership of a file                                             |
| `dd`      | Copies data from an input to an output                                      |
| `pwd`     | Displays the name of the current directory                                  |
| `ps`      | Lists the processes currently running in the system                         |
| `su`      | Simulates a login as another user or to become a superuser                  |
| `sudo`    | Runs a command as a super user, by default, or another named user           |
| `grep`    | Used to search for specific strings of characters within files or outputs   |
| `ifconfig`| Display/configure network card info (deprecated, use `ip address`)          |
| `apt-get` | Install, configure and remove packages on Debian systems                    |
| `iwconfig`| Wireless configuration tool like `ifconfig` but for Wi-Fi                   |
| `shutdown`| Shutdown, restart, halt, sleep or log out users                             |
| `passwd`  | Used to change passwords                                                    |
| `cat`     | Displays contents of files                                                  |
| `man`     | Displays the documentation for a specific command                           |

---

## 📁 File and Directory Commands

| Command | Description                                                                 |
|---------|-----------------------------------------------------------------------------|
| `ls`    | Displays the files inside a directory                                       |
| `cd`    | Changes the current directory                                               |
| `mkdir` | Creates a directory under the current directory                             |
| `cp`    | Copies files from source to destination                                     |
| `mv`    | Moves or renames files and directories                                      |
| `rm`    | Removes files                                                               |
| `grep`  | Searches for specific strings of characters within a file or outputs        |
| `cat`   | Lists the contents of a file and expects the file name as the parameter     |

---

## 🌐 Servers, Services, and Their Ports

| Port     | Description                                  |
|----------|----------------------------------------------|
| 20/21    | File Transfer Protocol (FTP)                 |
| 22       | Secure Shell (SSH)                           |
| 23       | Telnet remote login service                  |
| 25       | Simple Mail Transfer Protocol (SMTP)         |
| 53       | Domain Name System (DNS)                     |
| 67/68    | Dynamic Host Configuration Protocol (DHCP)   |
| 69       | Trivial File Transfer Protocol (TFTP)        |
| 80       | Hypertext Transfer Protocol (HTTP)           |
| 110      | Post Office Protocol version 3 (POP3)        |
| 123      | Network Time Protocol (NTP)                  |
| 143      | Internet Message Access Protocol (IMAP)      |
| 161/162  | Simple Network Management Protocol (SNMP)    |
| 443      | HTTP Secure (HTTPS)                          |

---

## 📜 Monitoring Service Logs

Log files are the records that a computer stores to track events.

### Types of Logs:
- Application logs
- Event logs
- Service logs
- System logs

### Common Log Files

| Log File                        | Description                                                                                       |
|--------------------------------|---------------------------------------------------------------------------------------------------|
| `/var/log/messages`            | Generic computer activity logs (non-critical system messages)                                    |
| `/var/log/syslog`              | Debian equivalent of `/var/log/messages`                                                         |
| `/var/log/auth.log`            | Authentication logs in Debian/Ubuntu                                                             |
| `/var/log/secure`              | Authentication logs in RedHat/CentOS                                                              |
| `/var/log/boot.log`            | Stores messages logged during system startup                                                     |
| `/var/log/dmesg`               | Kernel ring buffer messages — low-level hardware logging                                         |
| `/var/log/kern.log`            | Logs from the kernel                                                                             |
| `/var/log/cron`                | Stores cron job execution status and errors                                                      |
| `/var/log/mysqld.log`          | MySQL logs in RedHat-based systems                                                               |
| `/var/log/mysql.log`           | MySQL logs in Debian/Ubuntu systems                                                              |

---

## 🗃️ File System Types in Linux

### ext2, ext3, ext4
- ext2: No journaling, good for flash storage.
- ext3: Adds journaling, reduces corruption from crashes.
- ext4: Successor of ext3, supports larger files and better performance.

### Other File Systems
- **NFS**: Network-based file system.
- **CDFS**: File system for CDs.
- **Swap**: Used when RAM is full.
- **HFS+/APFS**: Apple file systems supported with Linux modules.

### Master Boot Record (MBR)
- Stores info on file system organization.
- Loads the OS by handing over to a bootloader.

---

## 🔐 Linux Roles and File Permissions

Every file has permissions for user, group, and others: **Read (r), Write (w), Execute (x)**.

### Example:
```bash
ls -l space.txt
```

Output:
```
-rwxrw-r-- 1 analyst staff 253 May 20 12:49 space.txt
```

Explanation of fields:
1. `-` → This is a file (if `d` it's a directory)
2. `rwx` → User permissions: read, write, execute
3. `rw-` → Group permissions: read, write
4. `r--` → Other users: read-only
5. `1` → Number of hard links
6. `analyst` → Owner
7. `staff` → Group
8. `253` → File size in bytes
9. `May 20 12:49` → Last modified date/time
10. `space.txt` → File name

### 🧮 Permission Representation

| Binary | Octal | Permission | Description            |
|--------|-------|------------|------------------------|
| 000    | 0     | ---        | No access              |
| 001    | 1     | --x        | Execute only           |
| 010    | 2     | -w-        | Write only             |
| 011    | 3     | -wx        | Write and Execute      |
| 100    | 4     | r--        | Read only              |
| 101    | 5     | r-x        | Read and Execute       |
| 110    | 6     | rw-        | Read and Write         |
| 111    | 7     | rwx        | Read, Write, Execute   |

Root user can override all permissions.

---

## 🧩 Installing and Running Applications on a Linux Host

Applications are installed as **packages** using **package managers**. These handle placing files in correct locations.

### 🛠️ Package Managers
- `apt` / `dpkg`: Used in Debian, Ubuntu, and Kali
- `pacman`: Used in Arch Linux

### Common apt Commands
```bash
sudo apt-get update     # Updates package list
sudo apt-get upgrade    # Upgrades installed packages
```

Package managers simplify installing complex compiled programs and manage dependencies for you.
