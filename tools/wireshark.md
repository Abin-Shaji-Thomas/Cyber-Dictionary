# 🧠 Wireshark Master Reference Guide (`tools/wireshark.md`)

A complete walkthrough for Wireshark and `tshark` — installation, usage, filters, capture tips, and advanced analysis. This guide is meant for penetration testers, red teamers, network analysts, and cybersecurity interns.

---

## 📦 Installation (Kali Linux)

```bash
sudo apt update
sudo apt install wireshark -y
```

To run as non-root:

```bash
sudo dpkg-reconfigure wireshark-common
sudo usermod -aG wireshark $USER
newgrp wireshark
```

---

## 🖥️ Launching Wireshark GUI

```bash
wireshark &
```

---

## 🔍 What Wireshark Does

- Captures live network packets
- Displays layer-by-layer protocol data
- Allows real-time and post-capture analysis
- Supports **hundreds** of protocols (TCP, UDP, HTTP, DNS, TLS, ICMP, etc.)

---

## 📡 Capturing Packets

### Start live capture:

1. Open Wireshark
2. Choose a network interface (usually `eth0`, `wlan0`)
3. Click the blue shark fin (Start Capture)

---

## 🔎 Display Filters (Applied after capture)

| Purpose               | Filter                                   |
|-----------------------|------------------------------------------|
| IP address            | `ip.addr == 192.168.1.10`                |
| Source IP             | `ip.src == 192.168.1.10`                 |
| Destination IP        | `ip.dst == 192.168.1.10`                 |
| TCP traffic           | `tcp`                                    |
| UDP traffic           | `udp`                                    |
| HTTP only             | `http`                                   |
| DNS traffic           | `dns`                                    |
| Port 80 only          | `tcp.port == 80`                         |
| TCP + contains string | `tcp contains "login"`                   |
| Show only errors      | `tcp.analysis.flags`                     |
| Filter MAC address    | `eth.addr == 00:11:22:33:44:55`          |

---

## 🎯 Capture Filters (Before capture begins)

| Purpose         | Filter Example                 |
|-----------------|-------------------------------|
| Capture only TCP| `tcp`                         |
| Specific IP     | `host 192.168.1.5`            |
| Specific port   | `port 443`                   |
| IP range        | `net 192.168.1.0/24`         |
| Not a port      | `not port 22`                |

Set these in: **Capture → Options → Capture Filter**

---

## 📁 File Operations

```bash
# Open a .pcap file
wireshark capture.pcap

# Export packets
File → Export Specified Packets → Save as .pcapng/.txt/.csv
```

---

## 🛠 Useful Features

- **Follow TCP Stream:** Right-click → Follow Stream → TCP
- **Name resolution:** View → Name Resolution
- **Protocol hierarchy:** `Statistics → Protocol Hierarchy`
- **Conversation view:** `Statistics → Conversations`
- **I/O Graph:** `Statistics → I/O Graph`
- **Expert Info:** `Analyze → Expert Info`

---

## 🧵 Colorization

Wireshark uses color rules to highlight traffic:
- TCP traffic → green
- HTTP requests → light blue
- DNS queries → purple
Customize via: `View → Coloring Rules`

---

## 🧪 Analyzing Attacks

| Attack Type     | Filter / Behavior |
|-----------------|-------------------|
| ARP spoofing    | Look for duplicate IP with different MACs |
| DNS poisoning   | Check for suspicious DNS responses         |
| TCP Reset Attack| Look for `RST` flags                       |
| DoS             | High rate of SYN, ICMP, or malformed packets |
| Credential Leak | Filter `http.request.method == "POST"` and follow stream |

---

## 🧰 CLI Version: `tshark`

### Capture to file:

```bash
sudo tshark -i eth0 -w output.pcap
```

### Display in console:

```bash
sudo tshark -i wlan0 -Y "http"
```

### Read existing capture:

```bash
tshark -r capture.pcap
```

### Use filter:

```bash
tshark -r file.pcap -Y "ip.src == 10.0.0.1 && tcp.port == 80"
```

---

## 🪄 Cheatsheet

```bash
# Capture HTTP GET requests
http.request.method == "GET"

# Show SSL/TLS handshakes
ssl.handshake

# Filter FTP passwords
ftp.request.command == "PASS"

# Only SYN packets
tcp.flags.syn == 1 && tcp.flags.ack == 0

# Detect DoS - lots of SYN, no ACK
tcp.analysis.retransmission
tcp.analysis.flags
```

---

## 🔐 Tips for Ethical Use

- Only capture traffic you’re authorized to monitor
- Avoid storing passwords or credentials in saved .pcap files
- Anonymize sensitive IPs when sharing reports

---

## 📚 Further Learning

- [Wireshark Official Docs](https://www.wireshark.org/docs/)
- [Protocol Examples](https://wiki.wireshark.org/)
- [tshark man page](https://www.wireshark.org/docs/man-pages/tshark.html)

---

## ✅ Summary

Wireshark is your **deep packet inspection powerhouse**. Pair it with `tshark`, filters, and a sharp mind to become unstoppable in:
- Network recon
- Malware analysis
- Red teaming
- Incident response

---
