## 🚀 Installing `.sh` Files in Kali Linux (Example: OWASP ZAP)

### 🔹 Step 1: Go to the folder
```bash
cd ~/Downloads
```

### 🔹 Step 2: Make the file executable
```bash
chmod +x ZAP_2_16_1_unix.sh
```

### 🔹 Step 3: Run the installer
```bash
./ZAP_2_16_1_unix.sh
```

Follow the GUI installer.

---

### 🔹 Step 4: Create a Desktop Shortcut
```bash
sudo nano /usr/share/applications/zap.desktop
```

Paste:
```ini
[Desktop Entry]
Name=OWASP ZAP
Comment=Web Application Security Scanner
Exec=/home/your_username/ZAP_2.16.1/zap.sh
Icon=/home/your_username/ZAP_2.16.1/zap.ico
Terminal=false
Type=Application
Categories=Development;Security;
```

> Replace `your_username` with the result of `whoami`.

Save:
- `CTRL + O` → Enter  
- `CTRL + X` → Exit

Update launcher index:
```bash
sudo update-desktop-database
```

---

### 🔹 Launch ZAP

Search for **ZAP** in the app menu or run:
```bash
/home/abin/ZAP_2.16.1/zap.sh
```
