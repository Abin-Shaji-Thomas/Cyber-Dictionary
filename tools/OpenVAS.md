# 🛡️ OpenVAS (Greenbone Vulnerability Management) — Complete Guide

> **Tool Category**: Vulnerability Scanner  
> **Platform**: Linux (Kali Recommended)  
> **Level**: Intermediate – Advanced  
> **Maintainer**: Greenbone GmbH  
> **Tool Purpose**: To detect, assess, and report security vulnerabilities in networks, devices, servers, and services.

---

## 📘 Introduction

OpenVAS (now known as part of **Greenbone Vulnerability Management - GVM**) is a **professional-grade vulnerability scanner**, similar to Nessus and Qualys, but open-source and fully free.

It is used by cybersecurity professionals and ethical hackers to:
- Scan hosts and networks for vulnerabilities
- Identify misconfigurations, outdated software, and CVEs
- Generate risk reports based on CVSS (vulnerability severity scoring)

---

## ⚙️ Installation (Kali Linux)

Kali includes `gvm` by default, but it can be manually installed and fixed if needed.

### 🔧 Step-by-Step Install

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install gvm -y
sudo gvm-setup
```

### 📌 Fix for Feed Collation Version Errors

If you get `REFRESH COLLATION VERSION` errors, fix with:

```bash
sudo -u postgres psql
```

In `psql`, run:

```sql
ALTER DATABASE template1 REFRESH COLLATION VERSION;
ALTER DATABASE postgres REFRESH COLLATION VERSION;
ALTER DATABASE template0 REFRESH COLLATION VERSION;
\q
```

Then run:

```bash
sudo runuser -u _gvm -- gvmd --create-user=admin --password=password
sudo gvm-setup
```

---

## 🚀 Starting and Stopping OpenVAS

```bash
# Start all services (scanner + web UI + DB)
sudo gvm-start

# Stop all GVM services safely
sudo gvm-stop

# Confirm nothing is running
ps aux | grep gvm
```

---

## 🌐 Access Web Interface

Open your browser:

```
https://127.0.0.1:9392
```

Login:
- **Username**: `admin`
- **Password**: `password`

Accept the SSL warning.

---

## 🧪 Usage: Performing a Vulnerability Scan

### 1. 🎯 Create a Scan Target

> Menu: `Configuration → Targets → Create Target`

| Field | Value |
|-------|-------|
| Name  | My Router |
| Hosts | (your desired IP) |
| Port list | Default |

---

### 2. 📊 Create a Scan Task

> Menu: `Scans → Tasks → Create Task`

| Field | Value |
|-------|-------|
| Name | Full Scan - Router |
| Target | Choose from step 1 |
| Scan Config | Full and fast |

---

### 3. ▶️ Start the Scan

> Menu: `Scans → Tasks`  
Click ▶️ next to your task name.

Status will go from `New → Requested → Running → Done`.

---

### 4. 📄 View Report

> Menu: `Scans → Reports → Click your report`

You’ll see:
- CVEs found
- Risk classification: Low, Medium, High, Critical
- Host summary
- Export options: PDF, HTML, XML

---

## 📁 Export Report

Once a scan is complete, you can **download the report**:

> `Reports → Download → Choose PDF or HTML`

---

## 📂 Important Commands and Logs

| Task | Command |
|------|---------|
| View logs live | `sudo tail -f /var/log/gvm/gvmd.log` |
| Scanner status | `sudo systemctl status ospd-openvas` |
| Manual restart | `sudo pkill ospd-openvas && sudo gvm-start` |
| Manual socket test | `ls -l /run/ospd/ospd-openvas.sock` |
| List scanners | `sudo runuser -u _gvm -- gvmd --get-scanners` |

---

## 🧠 Notes & Tips

- OpenVAS may take 5–15 minutes to scan even small networks.
- Scanner may appear stuck at `0%` — let it run.
- Best used for **internal infrastructure, routers, test servers**.
- Use `nmap` beforehand to check open ports and confirm target.
- GVM requires **8GB+ RAM**, **60GB+ disk** ideally for fast sync and scanning.

---

## ❌ Common Errors & Fixes

| Error | Fix |
|-------|-----|
| `Feed owner is not set` | Set UUID manually via `gvmd --modify-setting` |
| `Play button greyed` | Scanner not attached — assign scanner in task settings |
| No scan progress | Let it run, check logs with `tail -f /var/log/gvm/gvmd.log` |
| Socket not created | Manually run `ospd-openvas` with full path |
| Web UI unreachable | Ensure `gvm-start` completed and port `9392` is open |

---

## 📚 Real-World Use Cases

- Auditing company LAN/wifi routers  
- Performing vulnerability management in SOC teams  
- Scanning web servers for unpatched CVEs  
- Risk scoring internal assets during red team assessments

---

## ✅ Summary

| Feature | Detail |
|---------|--------|
| Tool Type | Vulnerability Scanner |
| License | Open Source |
| Interface | Web + CLI |
| Main Commands | `gvm-start`, `gvm-stop`, `gvmd`, `ospd-openvas` |
| Report Types | PDF, HTML, XML |
| Detection Level | CVE, Service Misconfig, SSL Issues |

---

## 🧠 Bonus: Combine With

| Tool | Use |
|------|-----|
| 🔎 `nmap` | Discover open ports before scanning |
| 🔐 `wireshark` | Monitor network while scan is running |
| 🛡️ `firejail` | Isolate GVM components |
| 📦 `docker` | Run scans from isolated containers |

---

## 🏁 Author Notes

This markdown was generated for **CyberBible** by Abin Shaji Thomas & 🐉 Kali GPT.  
OpenVAS is a complex but powerful tool — use it ethically, learn it deeply, and you're one step closer to mastering vulnerability assessment.

---
