## 📦 Install `.tar.xz` Apps (Example: Telegram)

### 🔹 Step 1: Extract the Archive
```bash
# Go to your Downloads folder (or wherever the file is)
cd ~/Downloads

# Extract the .tar.xz archive
tar -xf tsetup.5.15.2.tar.xz
```

This creates a folder named `Telegram`.

---

### 🔹 Step 2: Run the App
```bash
cd Telegram
./Telegram
```
Telegram will now launch. It runs as a **portable app** — no need for full system installation.

---

### 🔹 Step 3 (Optional): Move App to `/opt/` for Global Access
```bash
sudo mv ~/Downloads/Telegram /opt/telegram
```
Now the app is in a standard Linux directory used for third-party software.

---

### 🔹 Step 4: Create a System Shortcut (Desktop Entry)
```bash
sudo nano /usr/share/applications/telegram.desktop
```

Paste the following into the file:
```ini
[Desktop Entry]
Name=Telegram
Comment=Telegram Desktop Messaging App
Exec=/opt/telegram/Telegram
Icon=/opt/telegram/telegram.png
Terminal=false
Type=Application
Categories=Network;InstantMessaging;
```

> ✅ Make sure the `Exec` and `Icon` paths match your system.

Save and close:
- Press `CTRL + O` → Enter  
- Press `CTRL + X` → Exit

Then update the desktop database:
```bash
sudo update-desktop-database
```

---

### 🔹 Step 5: Add to Favorites or Search Menu
Now you can:
- Search for **Telegram** in your app menu
- Right-click → **Add to Favorites**

---

### 🔹 Bonus: Get Your Username (for fixing path issues)
```bash
whoami
```
Use this if you're unsure what to replace in `/home/your_username/`.

---

✅ **Telegram is now installed with a working launcher shortcut!**
