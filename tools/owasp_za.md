# 🧪 OWASP ZAP - Complete Offensive Toolkit Guide (`tools/owasp_zap.md`)

> Master offensive web app security scanning with OWASP ZAP — GUI, CLI, and automation workflows designed for penetration testers, red teamers, and bug bounty hunters.

---

## 📦 1. Installation

### 🐧 Kali Linux (CLI Install)
```bash
sudo apt update
sudo apt install zaproxy -y
```

### 🧊 Universal (Download Script)
```bash
wget https://github.com/zaproxy/zaproxy/releases/download/v2.14.0/ZAP_2.14.0_unix.sh
chmod +x ZAP_2.14.0_unix.sh
./ZAP_2.14.0_unix.sh
```

---

## 🚀 2. Launching ZAP

```bash
zaproxy &
```

or:

```bash
/home/$USER/ZAP_2.14.0/zap.sh
```

---

## 🎛️ 3. Interface Overview

| Component           | Description                              |
|---------------------|------------------------------------------|
| Sites Tree          | Hosts and discovered endpoints           |
| History             | List of requests and responses           |
| Request/Response    | Raw HTTP data                            |
| Spider              | Crawls target links                      |
| Active Scan         | Injects payloads for vulnerabilities     |
| Alerts              | Found vulnerabilities sorted by risk     |
| Break              | Allows intercept and modification        |

---

## 🌐 4. Basic Scan Workflow (GUI)

1. Open ZAP
2. Go to `Quick Start > Automated Scan`
3. Enter URL (e.g. `http://localhost:8082/WebGoat`)
4. Click **"Attack"**
5. View results in **Alerts**

---

## 🧭 5. Modes

| Mode        | Description                            |
|-------------|----------------------------------------|
| Safe        | Passive scanning only                  |
| Protected   | Passive + Active only for defined scope|
| Standard    | Full power                              |
| Attack      | Auto spider + active scan              |

Change via: `Top Bar → Mode → [Select]`

---

## 🕷️ 6. Spidering Targets

- Go to `Sites > Right-click Target > Attack > Spider`
- Crawls all links
- Useful before active scanning

---

## 💥 7. Active Scanning (Manual)

- Right-click target → `Attack > Active Scan`
- Select policy:
  - SQL Injection
  - XSS
  - CSRF
  - Server Misconfig
- Watch vulnerabilities appear in **Alerts**

---

## 🔥 8. Manual Testing Tools

- ⚡ **Fuzzer**: Right-click → Fuzz input field → Use built-in payloads
- 📤 **Request Editor**: Modify requests → resend
- 📊 **Breakpoints**: Intercept & edit requests before sending
- 🧪 **Authentication**: Add Login Scripts or Session Detection

---

## 🔐 9. Authentication Testing

1. Go to `Tools > Options > Authentication`
2. Set:
   - **Login URL**
   - **POST data**
   - **Username/Password field names**
3. Enable Session Management (cookies or headers)

Example: Authenticated scan on DVWA or WebGoat

---

## 📄 10. Report Generation

### From GUI:
- `File → Report → Generate HTML`
- Choose format: HTML, XML, JSON

### From CLI:
```bash
zap-cli report -o report.html -f html
```

---

## ⚙️ 11. Scripting & Automation

### 📜 Scripts:
- Load from `Tools > Scripting`
- Use for custom auth, injection logic, etc.

### ⚙️ CLI:
```bash
zap.sh -cmd -quickurl http://target -quickout zap_report.html
```

### 🧠 API Access:
- Enable via `Tools > API`
- Access at: `http://localhost:8080/JSON/`
- Integrate with CI/CD

---

## 🛡️ 12. Common Use Cases

| Goal                      | Action                            |
|---------------------------|-----------------------------------|
| Scan Localhost Site       | Add `localhost` to scope          |
| Authenticated Scan        | Set login + session handling      |
| Test for SQLi             | Scan URL with `id=` parameter     |
| Catch XSS                 | Look in alerts → `Reflected XSS` |
| Intercept & Modify        | Use Breakpoints                   |
| File Upload Attacks       | Use Fuzzer on file parameters     |

---

## 🧪 13. Intern Projects You Can Try

- Scan `WebGoat` and capture:
  - SQL Injection
  - XSS
  - CSRF
- Perform Authenticated scan of DVWA
- Generate professional HTML report for mentor
- Use Fuzzer to attack input fields manually

---

## 💣 14. Common Filters (Alert Tab)

| Severity   | Filter Value      |
|------------|-------------------|
| High       | `risk == High`    |
| Medium     | `risk == Medium`  |
| Low        | `risk == Low`     |
| Info       | `risk == Informational` |
| Plugin ID  | `pluginId == 40012` (XSS) |

---

## 🧠 15. Pro Tips

- Set ZAP proxy in browser: `127.0.0.1:8080`
- Use **Scope mode** to limit attacks
- Regularly update ZAP plugins via `Help → Check for Updates`
- Use in combination with BurpSuite, Nikto, Nmap

---

## 📚 16. Resources

- [ZAP User Guide](https://www.zaproxy.org/docs/)
- [ZAP GitHub Repo](https://github.com/zaproxy/zaproxy)
- [ZAP Scripts Hub](https://github.com/zaproxy/community-scripts)
- [ZAP API Docs](https://www.zaproxy.org/docs/api/)

---

## ✅ Summary

OWASP ZAP is a powerful open-source DAST tool that enables full web app attack surface mapping and exploitation in both manual and automated modes.

> From interns to pros — ZAP is a must in every red team toolbox 🐉

---
