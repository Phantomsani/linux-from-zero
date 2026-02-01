# 🐧 Linux From Zero — Day 1 Journey (Ubuntu + Termux Style Setup)

> A complete beginner’s first-day journey into **real Linux**  
> From **zero experience** → **working Ubuntu environment**  
> With a **Termux-style toolchain**, Python venv, and health-check automation.

---

## 👤 Author
**Name:** Sani  
**Background:** No prior Linux or coding experience  
**Goal:** Software / Computer Engineer → Kali Linux (later)  
**OS:** Ubuntu 24.04 LTS (VirtualBox on Windows 11)

---

## 🎯 Why This Repository Exists

This repo documents my **Day 1 Linux journey** so that:
- I can track my own progress
- Beginners can follow a **safe, proven path**
- Termux users can transition to **real Linux**
- Mistakes, fixes, and best practices are clearly explained

If you are:
- New to Linux  
- Coming from **Termux**
- Afraid of breaking your system  

👉 This repo is for you.

---

## 🧱 Environment Setup

### 💻 Host System
- Windows 11
- 16 GB RAM
- 512 GB NVMe SSD

### 🖥️ Virtual Machine
- Oracle VirtualBox
- Ubuntu **24.04 LTS Desktop**
- Guest Additions installed (display, clipboard, performance)

---

## ⌨️ Essential Linux Shortcuts

| Action | Shortcut |
|-----|---------|
| Open terminal | `Ctrl + Alt + T` |
| Stop command | `Ctrl + C` |
| Clear screen | `Ctrl + L` |
| Auto-complete | `Tab` |
| Copy (terminal) | `Ctrl + Shift + C` |
| Paste (terminal) | `Ctrl + Shift + V` |
| Release mouse (VM) | `Right Ctrl` |

---

## 📁 Core Linux Commands Learned

```bash
pwd
ls
cd
mkdir
touch
cp
mv
rm
cat
nano
chmod
whoami
uname -a
```
Key lesson:
Linux is about understanding, not memorizing commands.


🧰 ALL-IN-ONE TOOL INSTALL (TERMUX-STYLE)
✅ One-Command Ubuntu Setup
```
sudo apt update -y && sudo apt upgrade -y && \
sudo apt install -y \
git \
python3 python3-pip python3-venv python3-full \
php \
ruby \
nano \
bash \
curl \
wget \
openssh-client openssh-server \
figlet \
toilet \
tmux \
htop \
neofetch && \
sudo apt autoremove -y
```

🐍 Python Setup (Correct Linux Way)

Ubuntu 24.04 blocks global pip installs (PEP 668).
The correct approach is virtual environments.

🔹 Create Python Virtual Environment
```
python3 -m venv ~/pyenv
```
🔹 Activate Environment
```
source ~/pyenv/bin/activate
```
🔹 Install Python Packages 
```
pip install requests beautifulsoup4 mechanize rich future
```
🔹 Deactivate
```
deactivate
```
🧪 Tool Verification (Manual)
Check system tools
```
git --version
curl --version
wget --version
nano --version
bash --version
php -v
ruby -v
ssh -V
figlet -v
toilet -v
```
Check paths
```
which git
which python3
which pip3
```
🧪 Health-Check Script (Automation)
📄 Create script
```
nano health-check.sh
```
📌 Script content
```
#!/bin/bash

echo "===== SYSTEM TOOLS CHECK ====="
for cmd in git curl wget nano bash php ruby ssh figlet toilet python3 pip3; do
  command -v $cmd >/dev/null && echo "✔ $cmd installed" || echo "❌ $cmd missing"
done

echo
echo "===== PYTHON VENV CHECK ====="
if [ -d "$HOME/pyenv" ]; then
  source ~/pyenv/bin/activate
  python - <<EOF
pkgs = ["requests","bs4","mechanize","rich","future"]
ok=True
for p in pkgs:
    try:
        __import__(p)
        print(f"✔ {p} installed")
    except ImportError:
        print(f"❌ {p} missing")
        ok=False
if ok:
    print("ALL PYTHON PACKAGES OK")
EOF
  deactivate
else
  echo "❌ pyenv not found"
fi
```
▶️ Run it
```
chmod +x health-check.sh
./health-check.sh
```

🚀 Current Status

✅ Ubuntu installed & optimized
✅ Termux-style environment recreated correctly
✅ Python venv working
✅ Tools verified automatically
✅ Ready for deeper Linux learning
