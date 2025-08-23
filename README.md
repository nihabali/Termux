# 🐧 Debian + XFCE Desktop + VNC on Android (via Termux)

এই README-তে দেখানো হয়েছে কিভাবে **Termux** ব্যবহার করে **Debian Linux + XFCE Desktop** মোবাইলে ইন্সটল করা যায় এবং **VNC Viewer** দিয়ে ডেস্কটপ চালানো যায়।  
👉 এটি সবচেয়ে সহজ **root-only মেথড** (কোনো আলাদা ইউজার তৈরির ঝামেলা নেই)।  

---

## 📌 যা লাগবে
- **অ্যাপস:**
  - [Termux](https://f-droid.org/en/packages/com.termux/) (F-Droid/GitHub থেকে; Play Store-এও পাওয়া যায়)
  - [VNC Viewer](https://play.google.com/store/apps/details?id=com.realvnc.viewer.android) (বা bVNC)
- **স্টোরেজ:** অন্তত 4–6 GB ফ্রি
- **ইন্টারনেট:** ভালো কানেকশন

---

## 🚀 ধাপে ধাপে ইন্সটলেশন

### 1) Termux প্রাথমিক সেটআপ
```bash
pkg update && pkg upgrade -y
termux-setup-storage


---

2) proot-distro ইনস্টল ও Debian বসানো

pkg install -y proot-distro
proot-distro install debian


---

3) Debian-এ ঢোকা

proot-distro login debian


---

4) Debian আপডেট + ডেস্কটপ + VNC ইন্সটল

apt update && apt full-upgrade -y
apt install -y xfce4 xfce4-goodies dbus-x11 tigervnc-standalone-server


---

5) VNC সার্ভার চালু করা

vncserver -localhost :1

প্রথমবার VNC password চাইবে (৬–৮ অক্ষর) → সেট করে দাও

view-only password চাইলে → n চাপো



---

6) VNC Viewer অ্যাপ দিয়ে কানেক্ট করা

Address: localhost:1 (বা 127.0.0.1:5901)

Name: যেকোনো নাম

Password: যেটা সেট করেছিলে



---

📖 প্রতিদিন ব্যবহার

চালু করতে:

proot-distro login debian
vncserver -localhost :1

বন্ধ করতে:

vncserver -kill :1
exit

রিস্টার্ট করতে:

vncserver -kill :1
vncserver -localhost :1


---

⚙️ দরকারি টিপস

রেজোলিউশন বদলাতে:

vncserver -localhost :1 -geometry 1280x720 -depth 24

পাসওয়ার্ড পাল্টাতে:

vncpasswd

Debian থেকে বের হতে:

exit

Debian একেবারে রিমুভ করতে:

proot-distro remove debian



---

✅ দ্রুত চেকলিস্ট (মেমোরি শর্টকাট)

# Termux-এ একবার চালাও
pkg update && pkg upgrade -y
termux-setup-storage
pkg install -y proot-distro
proot-distro install debian
proot-distro login debian
apt update && apt full-upgrade -y
apt install -y xfce4 xfce4-goodies dbus-x11 tigervnc-standalone-server
vncserver -localhost :1

# প্রতিদিন চালাতে
proot-distro login debian
vncserver -localhost :1

# বন্ধ করতে
vncserver -kill :1
exit
