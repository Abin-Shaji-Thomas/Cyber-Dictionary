# 📦 Installing `.AppImage` Files on Kali Linux

## 🔸 What is an AppImage?

An `.AppImage` is a **portable executable** format for Linux that bundles an application and all its dependencies into a single file. It does **not require installation** or **root permissions**, and it works on most Linux distributions, including **Kali Linux**.

---

## ✅ How to Run `.AppImage` Files

### 1. **Download the AppImage**

Use `wget` or a browser to download the AppImage. Example:

```bash
wget https://github.com/flameshot-org/flameshot/releases/download/v12.1.0/Flameshot-12.1.0.x86_64.AppImage
```

### 2. **Make It Executable**

Set the execute permission:

```bash
chmod +x Flameshot-12.1.0.x86_64.AppImage
```

### 3. **Run the AppImage**

Execute the file directly:

```bash
./Flameshot-12.1.0.x86_64.AppImage
```

> 💡 Tip: You can move it to a permanent folder like `/opt/` or `~/Applications/` to keep things clean.

---

## 📌 Optional: Create a Menu Entry (Add to Application Launcher)

You can create a `.desktop` file to show the AppImage in your system menu.

### Step 1: Move the AppImage

```bash
sudo mv Flameshot-12.1.0.x86_64.AppImage /opt/flameshot.AppImage
```

### Step 2: Create a Desktop Entry

```bash
nano ~/.local/share/applications/flameshot.desktop
```

Paste this:

```ini
[Desktop Entry]
Name=Flameshot
Exec=/opt/flameshot.AppImage
Icon=flameshot
Type=Application
Categories=Utility;
```

### Step 3: Make Desktop File Executable

```bash
chmod +x ~/.local/share/applications/flameshot.desktop
```

### Step 4: (Optional) Refresh Desktop Menu

```bash
update-desktop-database ~/.local/share/applications/
```

Now you should see **Flameshot** in your application launcher.

---

## 🔄 Updating AppImages

### Option 1: Manual Update

1. Delete the old AppImage.
2. Download the new version.
3. Repeat the executable steps.

### Option 2: Built-in Updater (if supported)

```bash
./Flameshot-12.1.0.x86_64.AppImage --appimage-update
```

> ⚠️ Not all AppImages support auto-updates.

---

## 🧠 Bonus: Add to System PATH

If you want to run the AppImage like a normal Linux command:

```bash
sudo mv Flameshot-12.1.0.x86_64.AppImage /usr/local/bin/flameshot
```

Now run it from anywhere with:

```bash
flameshot
```

---

## 📚 Reference Links

- 🔗 [AppImage Official Site](https://appimage.org/)
- 🔗 [Flameshot GitHub Releases](https://github.com/flameshot-org/flameshot/releases)

---

> ✍️ Maintained by **Abin** — *CyberBible Documentation*  
> 🛡️ Kali Linux | Ethical Hacking | Cybersecurity Tools
