# 📦 Installing `.tar.xz` Apps on Kali Linux (With Start Menu & Icon)

This guide explains how to properly install applications distributed as `.tar.xz` files (like Telegram), and integrate them into the Kali Linux Start Menu with a working icon.

---

## 🔹 Step 1: Extract the `.tar.xz` Archive

```bash
# Go to your Downloads folder or the directory where the file is
cd ~/Downloads

# Extract the archive (example: Telegram)
tar -xf tsetup.5.15.2.tar.xz
```

This will create a folder (e.g., `Telegram`) containing the application files.

---

## 🔹 Step 2: Move the Folder to a Permanent Location

```bash
# Move it to /opt/ (common directory for third-party apps)
sudo mv Telegram /opt/telegram
```

> ✅ You can rename the folder to lowercase for consistency.

---

## 🔹 Step 3: Copy the Icon to a System Directory

Most `.tar.xz` apps include an icon inside the extracted folder. Find it and copy it:

```bash
# Copy icon to a shared location
sudo cp /opt/telegram/telegram.png /usr/share/pixmaps/telegram.png
```

> 🧠 If the icon has a different name or location, use `find` to locate it:
> ```bash
> find /opt/telegram -name "*.png"
> ```

---

## 🔹 Step 4: Create a Start Menu Entry (.desktop file)

```bash
sudo nano /usr/share/applications/telegram.desktop
```

Paste the following:

```ini
[Desktop Entry]
Name=Telegram
Comment=Telegram Desktop Messaging App
Exec=/opt/telegram/Telegram
Icon=/usr/share/pixmaps/telegram.png
Terminal=false
Type=Application
Categories=Network;InstantMessaging;
StartupWMClass=Telegram
```

> ✅ Make sure `Exec` points to the actual binary and `Icon` points to a valid `.png` file.

Save and close:
- Press `CTRL + O` → Enter  
- Press `CTRL + X` → Exit

---

## 🔹 Step 5: Update the Desktop Database

```bash
sudo update-desktop-database
```

This ensures your system recognizes the new launcher entry.

---

## 🔹 Step 6: Remove Duplicate or Broken Entries (Recommended)

Some `.tar.xz` apps (like Telegram) may auto-create a launcher in `~/.local/share/applications/`, which can cause **duplicate entries** or **broken icons**.

Clean them up:

```bash
rm -f ~/.local/share/applications/telegramdesktop.desktop
rm -f ~/.local/share/applications/userapp-Telegram*.desktop
```

---

## ✅ Done!

Now you can:

- Launch the app from the **Start Menu**
- See the **correct icon**
- Right-click → **Add to Favorites** (optional)

---

## 🧠 Bonus: Get Your Username (to avoid path issues)

```bash
whoami
```

Use this if you're using `$HOME` or `/home/your_username/` paths in the `.desktop` file.

---

## 📚 Example Recap (Telegram)

| What                | Path                                      |
|---------------------|-------------------------------------------|
| Extracted Folder    | `/opt/telegram/`                          |
| Executable Path     | `/opt/telegram/Telegram`                 |
| Icon Path           | `/usr/share/pixmaps/telegram.png`        |
| Desktop Entry File  | `/usr/share/applications/telegram.desktop` |

---

> ✍️ Maintained by **Abin** — *CyberBible Documentation*  
> 🛡️ Kali Linux | Ethical Hacking | Cybersecurity Tools
