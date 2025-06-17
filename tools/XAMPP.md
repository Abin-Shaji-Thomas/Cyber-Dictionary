# 🔧 XAMPP – Web Server Stack for Cybersecurity Labs

> **Category**: Web Application Hosting / Pentest Labs  
> **Platforms**: Linux (Kali), Windows, macOS  
> **Use Case**: Hosting vulnerable apps like DVWA, bWAPP, Mutillidae for local testing

---

## 📘 What is XAMPP?

XAMPP is a free and open-source cross-platform web server solution stack package developed by Apache Friends, consisting of:

- **X**: Cross-platform
- **A**: Apache (Web server)
- **M**: MariaDB/MySQL (Database)
- **P**: PHP (Backend language)
- **P**: Perl (optional)

It allows you to locally host **vulnerable applications** or **custom PHP-based apps** on your machine, making it ideal for **cybersecurity testing labs.**

---

## 🔧 Installation (Linux)

### ✅ Download

Visit [apachefriends.org](https://www.apachefriends.org)  
Or:

```bash
wget https://downloadsapachefriends.global.ssl.fastly.net/8.2.12/xampp-linux-x64-8.2.12-0-installer.run
```

### ✅ Install

```bash
chmod +x xampp-linux-x64-8.2.12-0-installer.run
sudo ./xampp-linux-x64-8.2.12-0-installer.run
```

---

## ⚙️ Managing XAMPP (Linux CLI)

| Task             | Command                                  |
|------------------|-------------------------------------------|
| Start XAMPP      | `sudo /opt/lampp/lampp start`            |
| Stop XAMPP       | `sudo /opt/lampp/lampp stop`             |
| Restart XAMPP    | `sudo /opt/lampp/lampp restart`          |
| Start Apache     | `sudo /opt/lampp/lampp startapache`      |
| Start MySQL      | `sudo /opt/lampp/lampp startmysql`       |
| Launch GUI Panel | `sudo /opt/lampp/manager-linux-x64.run`  |

---

## 🗂️ Web App Deployment Path

```bash
/opt/lampp/htdocs/
```

To deploy an app:

```bash
cd /opt/lampp/htdocs
sudo git clone https://github.com/digininja/DVWA.git
sudo chown -R daemon:daemon DVWA
```

Access in browser:  
```
http://localhost/DVWA
```

---

## 🐬 MySQL Access via CLI

```bash
sudo /opt/lampp/bin/mysql -u root
```

> Default has no password unless you configure one.

---

## 🧪 Apps You Can Host

| App        | Description                             |
|------------|-----------------------------------------|
| DVWA       | Damn Vulnerable Web App                 |
| bWAPP      | Buggy Web App (all OWASP vulns)         |
| Mutillidae | OWASP-top-10 learning platform          |
| Juice Shop | OWASP modern vulnerable app (Node.js)   |
| Custom     | Host your own PHP/MySQL projects        |

---

## 🚫 Troubleshooting

| Issue                        | Fix                                           |
|-----------------------------|-----------------------------------------------|
| Port 80 busy                | `sudo systemctl stop apache2`                 |
| MySQL not starting          | `sudo pkill mysqld` or check logs             |
| File permission denied      | `sudo chown -R daemon:daemon /opt/lampp/htdocs/<folder>` |
| `allow_url_include` errors  | Edit `php.ini` under `/opt/lampp/etc/`        |

---

## 🛡️ XAMPP in Cybersecurity Labs

XAMPP is perfect for hosting:
- Vulnerable apps for ZAP/Burp scanning
- Internal-only testing targets
- Educational apps for OWASP Top 10
- Custom CTF or testing apps

---

## ✅ Summary Cheatsheet

```bash
# Download
wget https://...xampp-linux-x64-8.2.12-0-installer.run

# Install
chmod +x xampp-linux-*.run
sudo ./xampp-linux-*.run

# Manage
sudo /opt/lampp/lampp start
sudo /opt/lampp/lampp stop

# Web files
/opt/lampp/htdocs/
```

---

## 👨‍🏫 Maintained by:

Abin Shaji Thomas  
Guided by 🐉 Kali GPT | CyberBible Project  
Private use for ethical cybersecurity training

