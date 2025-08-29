# 🐧 Debian XFCE Desktop on Android (via Termux + VNC)

This guide shows how to install **Debian Linux with XFCE Desktop** inside **Termux** on Android, and run it with **VNC Viewer**.  

👉 Simple **root-only setup** – no extra user creation needed.  

---

## 📌 Requirements
- **Apps:**  
  - [Termux](https://f-droid.org/en/packages/com.termux/) (from F-Droid or GitHub; also available on Play Store)  
  - [VNC Viewer](https://play.google.com/store/apps/details?id=com.realvnc.viewer.android) (or bVNC)
- **Storage:** at least 4–6 GB free
- **Internet:** stable connection recommended

---

## 🚀 Installation Steps

### 1) Initial Termux Setup
```bash
pkg update && pkg upgrade -y
termux-setup-storage
```

### 2) Install proot-distro & Debian
```bash
pkg install -y proot-distro
proot-distro install debian
```

### 3) Enter Debian
```bash
proot-distro login debian
```

### 4) Update Debian + Install XFCE & VNC
```bash
apt update && apt full-upgrade -y
apt install -y xfce4 xfce4-goodies dbus-x11 tigervnc-standalone-server
```

### 5) Start VNC Server
```bash
vncserver -localhost :1
```

👉 First time, set a VNC password (6–8 characters).  
👉 For view-only password → press `n`.

### 6) Connect via VNC Viewer
- **Address:** `localhost:1` (or `127.0.0.1:5901`)  
- **Name:** Any name you like  
- **Password:** The one you created earlier  

---

## 📖 Daily Usage
🔹 **Start session**
```bash
proot-distro login debian
vncserver -localhost :1
```

🔹 **Stop session**
```bash
vncserver -kill :1
exit
```

🔹 **Restart session**
```bash
vncserver -kill :1
vncserver -localhost :1
```

---

## ⚙️ Useful Tips
- **Change resolution:**
```bash
vncserver -localhost :1 -geometry 1280x720 -depth 24
```
- **Change VNC password:**
```bash
vncpasswd
```
- **Exit Debian:**
```bash
exit
```
- **Remove Debian completely:**
```bash
proot-distro remove debian
```

---

## ✅ Quick Reference (Copy & Paste)
```bash
# One-time setup
pkg update && pkg upgrade -y
termux-setup-storage
pkg install -y proot-distro
proot-distro install debian
proot-distro login debian
apt update && apt full-upgrade -y
apt install -y xfce4 xfce4-goodies dbus-x11 tigervnc-standalone-server
vncserver -localhost :1

# Start daily
proot-distro login debian
vncserver -localhost :1

# Stop
vncserver -kill :1
exit
```

---

## 🎯 Notes
- Performance depends on your device’s CPU & RAM.  
- Recommended: close heavy apps before running.  
- If you want a lighter desktop, you can install **LXDE** or **MATE** instead of XFCE.  
