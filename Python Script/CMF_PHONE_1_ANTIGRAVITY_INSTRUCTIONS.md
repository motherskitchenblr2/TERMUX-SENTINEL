# 📱 CMF Phone 1 (Nothing Mobiles) — Antigravity CLI Setup & 50 GB Cloud Reclaim Guide

This guide is specifically crafted for **Antigravity CLI (Gemini 2.5 Pro / 3.8)** running in **Termux** on your **CMF Phone 1 by Nothing Mobiles** (128 GB ROM / 8 GB RAM, currently 7 GB free).

---

## 📋 Quick Handover: Copy-Paste Prompt for Antigravity CLI on CMF Phone 1

When you open Antigravity CLI in Termux on your CMF Phone 1, simply copy and paste this single prompt:

```text
Hello Antigravity! I have transferred my complete Termux Sentinel and Rclone suite from my Realme 12 Pro+ to this CMF Phone 1. 

Please perform the following autonomous setup tasks:
1. Verify terminal environment and storage access at /storage/emulated/0. (If needed, prompt me to grant termux-setup-storage).
2. Install prerequisites: ensure 'python' and 'rclone' are installed via pkg.
3. Run the automated restorer:
   bash "/storage/emulated/0/Workspace /TERMUX-SENTINEL/Python Script/install_or_restore.sh"
4. Verify Rclone is authenticated using the copied ~/.config/rclone/rclone.conf for 'pasha_gdrive' (Pasha0118@gmail.com). Test connection with 'rclone lsd pasha_gdrive:' and create the dedicated directory 'pasha_gdrive:CMF_BKP'.
5. Audit the local storage (current: ~7 GB free out of 128 GB). Identify the largest directories across /storage/emulated/0 (DCIM, Movies, Downloads, Pictures, WhatsApp Media, Telegram) and Termux/Ubuntu caches.
6. Launch the migration script 'nohup bash ~/migrate_to_cmf_bkp.sh > ~/rclone_cmf.log 2>&1 &' to begin streaming files to Google Drive in the background with termux-wake-lock enabled.
7. Launch Termux_Sentinel ('sentinel' or 'sentinel clean -y') to clean system caches and help me safely reclaim at least 50 GB of local storage.
```

---

## 🛠️ Step-by-Step Technical Execution for Antigravity CLI

If Antigravity CLI executes step-by-step, here is the exact execution workflow:

### Step 1: Storage Permission Preflight
```bash
# Verify shared storage access
ls -la /storage/emulated/0 >/dev/null 2>&1 || termux-setup-storage
```

### Step 2: Install Essential Packages
```bash
pkg update -y
pkg install -y python rclone proot-distro ncurses-utils
```

### Step 3: Run One-Tap Restorer
```bash
bash "/storage/emulated/0/Workspace /TERMUX-SENTINEL/Python Script/install_or_restore.sh"
```
*Restores:*
* `~/Termux_Sentinel.py`
* `~/.config/termux_sentinel/vault.json` (Includes WhatsApp, CMF_BKP, and Realme_BKP locked shields)
* `~/.shortcuts/3_Termux_Sentinel.sh` & `~/.shortcuts/Termux_Sentinel.sh`
* `~/.config/rclone/rclone.conf` (Authenticated for Pasha0118@gmail.com)
* `~/migrate_to_cmf_bkp.sh`

### Step 4: Verify Google Drive Connection & Create CMF_BKP
```bash
# Test connection to Google Drive
rclone lsd pasha_gdrive:

# Create dedicated cloud destination for CMF Phone 1
rclone mkdir pasha_gdrive:CMF_BKP
```

### Step 5: Audit Storage Breakdown (Target: 50+ GB Reclaim)
```bash
# Inspect overall disk usage
df -h /data /storage/emulated/0

# Find top storage consumers in Android storage
du -sh /storage/emulated/0/DCIM \
       /storage/emulated/0/Download \
       /storage/emulated/0/Movies \
       /storage/emulated/0/Pictures \
       /storage/emulated/0/Android/media/com.whatsapp \
       /storage/emulated/0/Telegram 2>/dev/null
```

### Step 6: Start Background Cloud Migration
```bash
nohup bash /data/data/com.termux/files/home/migrate_to_cmf_bkp.sh > /data/data/com.termux/files/home/rclone_cmf.log 2>&1 &
```
*Features:*
* Automated `termux-wake-lock` keeps transfer alive when phone screen locks.
* High-speed parallel transfers (4 parallel streams, 64 MB chunk sizes).
* Preserves symlinks as `.rclonelink`.
* Streams to `pasha_gdrive:CMF_BKP/`.

### Step 7: Launch Termux Sentinel
```bash
python3 ~/Termux_Sentinel.py
```
* Features dynamic auto-detection: Displays **`CMF PHONE 1 (NOTHING) HUD`**.
* Safely purges package caches, npm caches, pip caches, and old agent task logs.
* Checks rogue bot scripts and active background processes.
* Shields WhatsApp and cloud targets from accidental deletion.

---

## 🎯 How to Safely Reclaim 50+ GB on CMF Phone 1

Once `migrate_to_cmf_bkp.sh` uploads files to `pasha_gdrive:CMF_BKP`, free up the 50 GB:

1. **Camera Photos & 4K Videos (`DCIM/Camera`)**:
   - Check that `pasha_gdrive:CMF_BKP/DCIM` contains the files (`rclone check /storage/emulated/0/DCIM pasha_gdrive:CMF_BKP/DCIM --one-way`).
   - Use Android's built-in File Manager or Google Photos ("Free up space") to purge uploaded local camera media (typically frees **20–35 GB**).

2. **Downloaded Files & APKs (`Download/`)**:
   - Delete old APKs, heavy ZIP archives, and downloaded installers (typically frees **10–15 GB**).

3. **WhatsApp Video & Media Cache**:
   - Inside WhatsApp Settings ➔ Storage and data ➔ Manage storage: review and delete forwarded videos larger than 5 MB (already backed up in Google Drive, typically frees **10–20 GB**).

4. **Termux & PRoot System Caches**:
   - Inside `Termux_Sentinel.py`, tick all safe items (`[a]`) and press `[c]` to purge package build caches (frees **3–8 GB**).

**Result:** Local available space will increase from **7 GB** to **55–65+ GB free**!
