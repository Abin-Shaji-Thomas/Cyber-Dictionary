# 🛰️ Nmap – Complete Offensive Network Recon Guide (`tools/nmap.md`)

> Master the art of active and passive network scanning with Nmap — the most essential tool in every red teamer's arsenal.

---

## 📦 1. Installation

### Kali Linux
```bash
sudo apt update && sudo apt install nmap -y
```

### macOS
```bash
brew install nmap
```

### From Source
```bash
wget https://nmap.org/dist/nmap-<version>.tar.bz2
tar -xvjf nmap-<version>.tar.bz2
cd nmap-<version>
./configure
make
sudo make install
```

---

## 🚀 2. First Steps

### Find Your IP Address
```bash
ip a         # Linux
ifconfig     # Legacy
ipconfig     # Windows
```

---

## 🔍 3. Basic Usage

```bash
nmap <target>
```

Examples:
```bash
nmap 192.168.1.1
nmap scanme.nmap.org
```

---

## 🧭 4. Scan Types

| Type             | Option | Description                             |
|------------------|--------|-----------------------------------------|
| SYN Scan         | -sS    | Stealth scan (default for root)         |
| TCP Connect      | -sT    | Full TCP handshake (for non-root users) |
| UDP Scan         | -sU    | Detect UDP services                     |
| Ping Sweep       | -sn    | Check live hosts (no port scan)         |
| Xmas Scan        | -sX    | Firewall evasion scan                   |
| Null Scan        | -sN    | No flags set – stealth                  |
| FIN Scan         | -sF    | FIN-only packet                         |

---

## 🎯 5. Port & Service Recon

### Specify Ports
```bash
nmap -p 21,22,80,443 192.168.1.1
nmap -p- 192.168.1.1
```

### Service & Version Detection
```bash
nmap -sV 192.168.1.1
```

### OS Fingerprinting
```bash
nmap -O 192.168.1.1
```

### Aggressive Scan
```bash
nmap -A 192.168.1.1
```

---

## 🔥 6. Speed & Stealth

| Option  | Purpose                            |
|---------|------------------------------------|
| -T0     | Paranoid (avoid detection)         |
| -T4     | Fast (common for pentesting)       |
| -T5     | Insane (super fast, noisy)         |
| -Pn     | No ping (assumes host is up)       |
| -n      | No DNS resolution                  |

---

## 🧠 7. NSE – Nmap Scripting Engine

### Run All Vulnerability Scripts
```bash
nmap --script vuln 192.168.1.1
```

### Run Specific Script
```bash
nmap --script http-title -p 80 <target>
```

### Common Categories
- `default`
- `vuln`
- `auth`
- `exploit`
- `malware`
- `discovery`

---

## 📂 8. Multiple Targets

```bash
nmap 192.168.1.1 192.168.1.5
nmap 192.168.1.0/24
nmap -iL targets.txt
```

---

## 📤 9. Output Formats

```bash
nmap -oN normal.txt <target>
nmap -oG grepable.txt <target>
nmap -oX xmlfile.xml <target>
nmap -oA allformats <target>
```

---

## 💣 10. Offensive Use Cases

| Goal                     | Example Command                             |
|--------------------------|---------------------------------------------|
| Host Discovery           | `nmap -sn 192.168.1.0/24`                   |
| Full Recon               | `nmap -A 192.168.1.1`                       |
| Scan All Ports           | `nmap -p- 192.168.1.1`                      |
| Brute-force FTP          | `nmap --script ftp-brute -p 21 <target>`   |
| Web Vuln Scan            | `nmap --script http-vuln* -p 80 <target>`  |

---

## 🛠️ 11. Troubleshooting

| Issue                   | Fix                                |
|-------------------------|-------------------------------------|
| Host appears offline    | Use `-Pn`                          |
| Permission denied       | Run with `sudo`                    |
| Slow scan               | Use `-T4`                          |
| DNS resolution error    | Use `-n`                           |

---

## 🧾 12. Cheatsheet

```bash
nmap -sS -T4 <target>                      # Stealth scan
nmap -A -T4 <target>                       # Aggressive all-in-one
nmap -p- <target>                          # Scan all ports
nmap -sV -p 22,80,443 <target>             # Service version detection
nmap --script vuln <target>               # Vulnerability scan
nmap -oA scan-results <target>            # Save in all formats
```

---

## 🧪 13. Lab Projects

- Scan Metasploitable:
  ```bash
  nmap -A 192.168.56.101
  ```

- Web Vuln Enumeration:
  ```bash
  nmap -p 80 --script http-vuln* <target>
  ```

- UDP SNMP Check:
  ```bash
  nmap -sU -p 161 <target>
  ```

- FTP Bruteforce:
  ```bash
  nmap --script ftp-anon,ftp-brute -p 21 <target>
  ```

---

## 📚 14. Resources

- [Nmap Docs](https://nmap.org/book/)
- [NSE Scripts](https://nmap.org/nsedoc/)
- [TryHackMe Nmap Room](https://tryhackme.com/room/nmap)
- [HackTricks Nmap Cheatsheet](https://book.hacktricks.xyz/network-services-pentesting/nmap)

---

## ✅ Summary

Nmap is the go-to recon tool for discovering hosts, scanning services, fingerprinting OSes, and detecting vulnerabilities. Whether you're doing a CTF or real-world red teaming, it’s your map to the network battlefield.

> 🐉 "Scan like a shadow. Strike like a storm." – Kali GPT
