# 🐺 WebWolf – Complete Ethical Cybersecurity Tool Guide

> A full guide for ethical hackers, cybersecurity students, and penetration testing enthusiasts. This document covers everything you need to know about using, configuring, and learning from **WebWolf**, the support platform for WebGoat.

---

## 📖 What is WebWolf?

**WebWolf** is an intentionally vulnerable application created by OWASP to work alongside **WebGoat**. While WebGoat provides interactive security lessons, WebWolf acts as a companion server that simulates real-world services such as:

- 📨 Fake email inboxes
- 🗂️ File upload and download features
- 🔗 Phishing links
- 📬 Payload reception for SSRF/XSS
- 🧪 Realistic post-exploitation endpoints

WebWolf gives ethical hackers and learners an environment to **practice and test exploits beyond the browser**, helping you understand what happens **after an attack is successful**.

---

## 🔧 Prerequisites

Before installing WebWolf, ensure the following tools are installed on your Kali Linux system:

```bash
sudo apt update
sudo apt install docker.io docker-compose -y
sudo systemctl start docker
sudo systemctl enable docker
```

---

## 🚀 Installing WebGoat + WebWolf with Docker

WebWolf and WebGoat are bundled in a single image by OWASP. You only need one Docker command to start both services:

```bash
sudo docker run -d -p 8082:8080 -p 9092:9090 --name webgoat webgoat/webgoat
```

### Port Mappings:

| Service   | Internal Port | External Port | Purpose                        |
|-----------|----------------|---------------|--------------------------------|
| WebGoat   | 8080           | 8082          | Web app for learning security |
| WebWolf   | 9090           | 9092          | Simulated service endpoints   |

---

## 🌐 Accessing WebGoat & WebWolf

After running the container, open:

- WebGoat: [http://localhost:8082/WebGoat](http://localhost:8082/WebGoat)
- WebWolf: [http://localhost:9092/WebWolf](http://localhost:9092/WebWolf)

Login with your custom user or create one if prompted.

---

## 🧪 What Can You Do with WebWolf?

| Feature                          | Description                                                  |
|----------------------------------|--------------------------------------------------------------|
| 📩 View Inbox                    | See fake phishing emails sent during exercises               |
| 🔗 Access Phishing URLs          | Test phishing links generated from WebGoat lessons           |
| 📤 Upload Files                  | Simulate file upload vulnerabilities                         |
| 📬 Receive POST Requests         | Used for testing CSRF, SSRF, and XSS callbacks               |
| 🧾 View Logs                     | Helps debug your payloads and backdoor simulations           |

---

## 🔐 Real-World Ethical Use Cases

- **Email Spoofing Simulation**  
  Send a fake phishing email and monitor if the victim clicks using WebWolf’s mail service.

- **Malicious File Upload**  
  Upload a `.php` or `.jsp` backdoor (harmlessly in lab) and see how it’s stored or executed.

- **XSS Callback Collection**  
  Trigger an XSS payload in WebGoat that calls back to WebWolf, simulating data theft.

- **CSRF Proof of Concept**  
  Send a crafted POST request to WebWolf and analyze the impact of missing CSRF protection.

---

## 🧼 Stopping WebGoat & WebWolf Without Losing Data

To **temporarily shut down** both services **without deleting user data**, run:

```bash
sudo docker stop webgoat
```

This pauses the container. Your progress, login, and session files are safe.

---

## 🔁 Starting WebGoat & WebWolf Again

To resume your work later (e.g., next day):

```bash
sudo systemctl start docker
sudo docker start webgoat
```

Your existing users and lessons are still available.

---

## 💾 Backup (Optional but Recommended)

You can create a backup image of your container:

```bash
sudo docker commit webgoat webgoat-backup
```

This snapshot can be restored later if you delete the original.

---

## 🧨 Permanently Deleting WebGoat & WebWolf

If you want to **fully remove** WebGoat/WebWolf and all saved data:

```bash
sudo docker stop webgoat
sudo docker rm webgoat
sudo docker rmi webgoat/webgoat
```

> ⚠️ This will delete your user progress, session cookies, and uploaded files.

---

## 🧠 Tips for Students

- WebWolf is **not just a side tool** — it teaches post-exploitation and real-world behavior.
- Try using WebWolf with Burp Suite and ZAP to simulate advanced payloads.
- Always use WebWolf/WebGoat in **private**, non-production environments.
- Avoid sharing URLs or cookies from WebWolf labs publicly.

---

## 📚 Additional Learning Resources

- [OWASP WebGoat GitHub](https://github.com/WebGoat/WebGoat)
- [OWASP ZAP](https://www.zaproxy.org/)
- [Docker for Beginners](https://docs.docker.com/get-started/)
- [Web Application Security Testing Guide (OWASP)](https://owasp.org/www-project-web-security-testing-guide/)

---

## ✅ Summary

WebWolf is an essential part of any ethical hacker’s lab. Paired with WebGoat, it provides a **complete simulation environment** for understanding how web-based attacks can progress after exploitation.

Whether you are:
- Practicing CSRF or XSS callbacks  
- Analyzing phishing behaviors  
- Testing file upload weaknesses  
- Learning about how payloads work post-click...

WebWolf gives you a place to do it **safely, legally, and ethically**.

---

## 📝 Author Notes

This markdown file was created as part of a private ethical hacking knowledge base called **CyberBible**, maintained by Abin Shaji Thomas and intended to support other ethical cybersecurity learners in mastering tools through practical labs and self-guided study.

If you're reading this, remember:  
> **Train hard, hack ethically. 🛡️**

