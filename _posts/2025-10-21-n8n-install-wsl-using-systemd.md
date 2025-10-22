---
title: 'How to Install n8n on Windows Using WSL and Ubuntu (With Auto-Start Using systemd)'
date: 2012-08-14
permalink: /posts/2025/10/n8n-install-wsl-using-systemd/
tags:
  - n8n
  - Automation
  - WSL
  - Ubuntu
  - Windows
  - Systemd
  - BeginnerGuide
  - NoCode
  - WorkflowAutomation
  - NodeJS
  - TechTutorial
  - StudentDeveloper
  - LocalSetup
  - OpenSource
---

> **For absolute beginners — even if you're still in school!**

If you’ve heard about **n8n** (pronounced “n-eight-n”) and want to run it on your Windows computer, this guide is for you! We’ll use **Windows Subsystem for Linux (WSL)** with **Ubuntu**, and then set it up so it **starts automatically** every time your computer boots — using something called **systemd**.

Don’t worry if those words sound scary. We’ll go step by step, like building with LEGO blocks!

---

## 🧩 What is n8n?

**n8n** is a free and open-source tool that helps you connect different apps and services together — like sending a Slack message when you get a new email, or saving Gmail attachments to Google Drive. It’s like digital glue for your online tools!

---

## 🛠️ What You’ll Need

- A Windows 10 or Windows 11 computer
- Basic comfort using the command line (we’ll show you every command!)
- About 15–20 minutes of time

---

## ✅ Step 1: Install WSL and Ubuntu

WSL lets you run Linux (like Ubuntu) inside Windows — without needing a separate computer or virtual machine.

### 1. Open PowerShell as Administrator
- Press `Windows + S`, type **PowerShell**
- Right-click **Windows PowerShell** → **Run as administrator**

### 2. Install WSL with Ubuntu
Run this command:

```powershell
wsl --install -d Ubuntu
```

> This will download and install Ubuntu from the Microsoft Store.  
> You’ll be asked to **restart your computer** — go ahead!

### 3. After restart, finish Ubuntu setup
- A terminal window will pop up.
- Create a **username** (e.g., `istiyak`) and **password** (you won’t see typing — that’s normal!).
- Remember your password — you’ll need it later.

---

## ✅ Step 2: Update Ubuntu

Open **Ubuntu** from your Start Menu.

Run these commands one by one:

```bash
sudo apt update
sudo apt upgrade -y
```

> Type your password when asked (no stars or dots appear — just type and press Enter).

This makes sure your system has the latest updates.

---

## ✅ Step 3: Install Node.js

n8n runs on **Node.js**, so we need to install it.

Run these commands:

```bash
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
sudo apt install -y nodejs
```

Check if it worked:

```bash
node -v
npm -v
```

You should see version numbers like `v20.x.x` — great!

---

## ✅ Step 4: Install n8n

Now, install n8n globally using npm:

```bash
npm install -g n8n
```

That’s it! n8n is now installed.

Try running it manually to test:

```bash
n8n
```

You’ll see a message like:

```
n8n ready on http://localhost:5678
```

Open your web browser and go to: [http://localhost:5678](http://localhost:5678)

🎉 You should see the n8n welcome screen!

> Press `Ctrl + C` in the terminal to stop it for now.

---

## ✅ Step 5: Make n8n Start Automatically with systemd

Right now, you have to type `n8n` every time you want to use it. Let’s make it **start automatically** when WSL starts — using **systemd**.

> ⚠️ **Important**: By default, WSL doesn’t support systemd. But we can enable it!

### Enable systemd in WSL

1. Close all Ubuntu windows.
2. Open **Notepad** as Administrator.
3. Open this file:  
   `C:\Users\<YourWindowsUsername>\.wslconfig`  
   (If it doesn’t exist, create it.)

4. Paste this inside:

```ini
[wsl2]
systemd=true
```

5. Save the file.
6. Restart WSL by running in PowerShell (as admin):

```powershell
wsl --shutdown
```

Then reopen **Ubuntu** from the Start Menu.

Now check if systemd is running:

```bash
systemctl list-units --type=service | head
```

If you see a list of services — **systemd is working!** 🎉

---

## ✅ Step 6: Create a systemd Service for n8n

We’ll create a small config file so systemd knows how to run n8n.

### 1. Create the service file

Run this command:

```bash
sudo nano /etc/systemd/system/n8n.service
```

> This opens a text editor called `nano`.

### 2. Paste the following into the file:

```ini
[Unit]
Description=n8n workflow automation
After=network.target

[Service]
Type=simple
User=istiyak
ExecStart=/usr/bin/n8n
Restart=always
Environment=NODE_ENV=production
Environment=N8N_HOST=0.0.0.0
Environment=N8N_PORT=5678

[Install]
WantedBy=multi-user.target
```

> 🔁 **Important**: Replace `istiyak` with **your Ubuntu username** (the one you created in Step 1).

### 3. Save and exit
- Press `Ctrl + O` → press Enter to save
- Press `Ctrl + X` to exit

### 4. Enable and start the service

Run these commands:

```bash
sudo systemctl daemon-reload
sudo systemctl enable n8n
sudo systemctl start n8n
```

Now n8n will:
- Start automatically when WSL starts
- Restart if it crashes
- Be available at [http://localhost:5678](http://localhost:5678)

Check if it’s running:

```bash
sudo systemctl status n8n
```

You should see **active (running)** in green.

---

## ✅ Step 7: Use n8n Anytime!

From now on:
- Just open **Ubuntu** (or even just use Windows!)
- Go to [http://localhost:5678](http://localhost:5678) in your browser
- Your n8n is already running — no extra commands needed!

> 💡 Tip: You don’t even need to keep the Ubuntu window open. As long as WSL is running (which it does in the background), n8n will work.

To stop it manually (if needed):

```bash
sudo systemctl stop n8n
```

To start again:

```bash
sudo systemctl start n8n
```

---

## 🎓 Summary (For Your Notes)

| Step | What You Did |
|------|--------------|
| 1 | Installed WSL + Ubuntu on Windows |
| 2 | Updated Ubuntu |
| 3 | Installed Node.js |
| 4 | Installed n8n |
| 5 | Enabled systemd in WSL |
| 6 | Created a systemd service to auto-start n8n |
| 7 | Now n8n runs automatically! |

---

## ❓ Common Questions

**Q: Do I need to keep Ubuntu open?**  
A: No! Once set up, n8n runs in the background. Just use your browser.

**Q: Can I access n8n from other devices on my network?**  
A: By default, no — it only listens on `localhost`. To change that, modify the `N8N_HOST` in the service file (advanced).

**Q: What if I get permission errors?**  
A: Make sure you used `sudo` where needed, and that your username in the service file matches your Ubuntu username.

---

## 🌟 You Did It!

Congratulations! You’ve just set up a powerful automation tool on your own computer — like a real developer. Whether you’re in middle school, high school, or beyond, this is a huge step into the world of tech.

Now go build your first workflow in n8n! 🚀

> Got stuck? Leave a comment below (if this were a real blog!) or ask a teacher, friend, or online community. Everyone starts somewhere.

Happy automating!  
— Istiyak
------