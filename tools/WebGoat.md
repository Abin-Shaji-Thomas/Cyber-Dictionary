# WebGoat – Full Documentation for Cybersecurity Lab Setup & Usage

**File:** `tools/webgoat.md`  
**Purpose:** Internal documentation for setting up, running, using, and managing the OWASP WebGoat platform in a professional cybersecurity learning environment.

---

## 1. Introduction

**WebGoat** is an open-source, deliberately insecure web application maintained by OWASP. It is designed to teach developers, testers, and cybersecurity students about web application vulnerabilities through hands-on lessons. Each module is structured around a specific vulnerability, aligned with the OWASP Top 10, and designed to be safely exploited in a controlled environment.

This document provides complete guidance for installing, managing, updating, and using WebGoat in a local lab using Docker, as well as proper usage patterns and professional-level best practices.

---

## 2. Use Case

- Learning OWASP Top 10 vulnerabilities
- Practicing ethical hacking in a sandbox environment
- Preparing for certifications (OSCP, CEH, etc.)
- Teaching students real-world vulnerability scenarios
- Running security workshops or internship training

---

## 3. System Requirements

- **Operating System:** Kali Linux, Parrot OS, or any Linux distro with Docker
- **Tools Needed:**
  - Docker
  - Browser (Firefox preferred)
  - Optionally: OWASP ZAP, Burp Suite for intercepts

---

## 4. Installation (Docker Method – Recommended)

### Step 1: Install Docker

```bash
sudo apt update
sudo apt install docker.io -y
sudo systemctl enable docker
sudo systemctl start docker
```

### Step 2: Pull and Run WebGoat

```bash
sudo docker run -d -p 8082:8080 -p 9092:9090 --name webgoat webgoat/webgoat
```

- `8080` (container) → `8082` (host) for WebGoat
- `9090` (container) → `9092` (host) for WebWolf

### Step 3: Access WebGoat

Open your browser and go to:

```
http://localhost:8082/WebGoat
```

---

## 5. Login and User Management

- **Default behavior:** You’ll be prompted to create a user.
- Use a test login like:
  - Username: `cyber-warrior`
  - Password: `education`
- This user will persist in the container unless the container is deleted.

---

## 6. Restarting WebGoat (Without Losing Data)

To safely **pause or stop** WebGoat:

```bash
sudo docker stop webgoat
```

To **resume** WebGoat later:

```bash
sudo docker start webgoat
```

> Your user data and challenge progress will remain intact.

---

## 7. Updating WebGoat

If a newer version is released:

```bash
sudo docker pull webgoat/webgoat
sudo docker stop webgoat
sudo docker rm webgoat
sudo docker run -d -p 8082:8080 -p 9092:9090 --name webgoat webgoat/webgoat
```

> **Note:** This will reset your existing data unless you create a persistent volume or commit a backup first.

---

## 8. Deleting WebGoat Completely

```bash
sudo docker stop webgoat
sudo docker rm webgoat
sudo docker rmi webgoat/webgoat
```

This will delete:
- All user data
- Saved lesson progress
- Logs

---

## 9. Common Problems and Fixes

| Issue | Solution |
|-------|----------|
| Port already in use | Use different host ports like 8083 or 9093 |
| Container name conflict | Rename container or remove old one |
| WebGoat not loading | Wait 30 seconds after container starts; check `docker logs webgoat` |
| "Unhealthy" container | Restart using `docker restart webgoat` |

---

## 10. WebGoat Modules Overview

Each lesson teaches a vulnerability by allowing the student to attack the application. Example modules:

| Vulnerability | Lesson Name |
|---------------|-------------|
| SQL Injection | "SQLi - Advanced", "String SQLi" |
| Cross-Site Scripting | "Reflected XSS", "DOM XSS" |
| Broken Access Control | "Session Hijack", "Forced Browsing" |
| CSRF | "Cross Site Request Forgery" |
| HTTP Proxy Attack | "Modify Method via Intercept" |
| Insecure Login | "Authentication Bypass" |

---

## 11. How to Work Through WebGoat

### A. Start with Basic Lessons:
- SQL Injection
- Reflected XSS
- CSRF

### B. Use DevTools or ZAP:
- Inspect network requests
- Modify cookies or headers
- Replay attacks

### C. Follow WebWolf Instructions (if integrated):
- Send phishing emails
- Upload payloads
- Submit responses to WebWolf server

---

## 12. Integrating with OWASP ZAP

To intercept WebGoat traffic:

1. Configure Firefox to use ZAP as proxy (127.0.0.1:8080)
2. Import ZAP's Root CA certificate into Firefox
3. Load WebGoat and complete lessons
4. Use ZAP’s Breakpoints to:
   - Pause requests
   - Modify headers
   - Change HTTP methods
5. Use ZAP scanner to passively analyze WebGoat vulnerabilities

---

## 13. Logging and Monitoring

To view logs from the container:

```bash
sudo docker logs webgoat
```

This shows:
- Server startup progress
- Application logs
- Errors (like misconfigured payloads or crashes)

---

## 14. Ethical Usage and Lab Environment Notes

- Do not expose WebGoat to a public network or server.
- Use only in **isolated environments** like localhost or VMs.
- Never use attack payloads from WebGoat against real websites or applications.
- Use it to understand, not exploit.

---

## 15. Screenshot Tips for Report Writing

Use tools like `flameshot` or `spectacle` to capture:

- Successful exploit messages
- Payloads in DevTools
- Intercepted requests via ZAP
- WebWolf interactions (like email view, uploads)

Organize screenshots with filenames like:
```
webgoat_sqli_success.png
webgoat_csrf_intercept.png
```

---

## 16. Saving Progress (Optional)

If you plan to shutdown or reset, commit the container:

```bash
sudo docker commit webgoat webgoat-backup
```

To restore it later:

```bash
sudo docker run -d -p 8082:8080 -p 9092:9090 --name webgoat-restored webgoat-backup
```

---

## 17. Alternatives to WebGoat

| Platform | Purpose |
|----------|---------|
| DVWA (Damn Vulnerable Web App) | Simpler but useful |
| Juice Shop (OWASP) | More realistic frontend |
| BWAPP | Great for broader vuln coverage |

Use them after mastering WebGoat.

---

## 18. Final Notes

WebGoat is a powerful, safe training ground to understand how web attacks work. It is best paired with tools like OWASP ZAP or Burp Suite and used alongside WebWolf for realistic exercises.

Always keep the following in mind:
- Document everything
- Learn responsibly
- Never test outside the lab
- Help others learn

---

## 19. Author Notes

This document was written as part of a private documentation initiative by Abin Shaji Thomas for the **CyberBible project**, designed to support ethical hacking education and structured, repeatable lab setups for red team development.

