# Spoolman Integration for Creality OS

A compatibility patch for the **Spoolman** component in Moonraker, specifically adapted for the modified, legacy Moonraker builds shipped with Creality OS.

> ⚠️ **Compatibility Note:** This patch was created and **tested on a Creality K2**. It should theoretically work on other Creality OS machines (K1, K1 Max, K1C) running the same Moonraker base. Feedback and test results for other models are welcome!

---

## 🛠️ Why This Fork Exists

Modern versions of Moonraker's official `spoolman.py` component rely on internal modules like `utils.common` (such as `RequestType` or `HistoryFieldData`) and recent API structures that do not exist in Creality's modified, older Moonraker release.

Attempting to drop the stock `spoolman.py` into Creality OS results in Python import crashes (`ImportError: cannot import name 'common' from 'utils'`).

This modified version:
- Removes external dependencies on missing `utils.common` modules.
- Inlines lightweight fallback implementations for required types (`RequestType`, `HistoryFieldData`).
- Safely handles optional components (such as announcement feeds) that might be missing or incomplete in Creality OS.
- Restores full **Spoolman** filament tracking functionality on Creality OS machines.

---

## 🚀 Installation Guide

### Prerequisites
- Root access enabled on your Creality printer via SSH.
- A running [Spoolman](https://github.com/Donnet99/spoolman) instance on your local network.

---

### Step 1: Download & Install the Component

Connect to your printer via SSH (`root@<your-printer-ip>`) and run:

```bash
# Navigate to Moonraker's components directory
cd /usr/share/moonraker/components/
```

# Backup any existing file (if present)
```bash
[ -f spoolman.py ] && mv spoolman.py spoolman.py.bak
```
# Download the patched spoolman.py
```bash
wget https://raw.githubusercontent.com/lucasbalon/moonraker-spoolman-creality/main/spoolman.py
```

---

### Step 2: Configure `moonraker.conf`

Edit your `moonraker.conf` file (located in your configuration folder or accessible via Mainsail / Fluidd / Creality Print):

Add the `[spoolman]` configuration block:

```ini
[spoolman]
server: http://<YOUR_SPOOLMAN_IP>:7912
# Sync rate in seconds (default: 5)
sync_rate: 5
```
---

### Step 3: Restart printer
```bash
reboot
```
---

## 🧪 Testing & Feedback

This component has been verified on:
- [x] **Creality K2** (Creality OS)
- [ ] **Creality K1 / K1 Max / K1C** *(Untested - feel free to open an issue or PR with your results!)*

---

## 📄 License

Distributed under the terms of the **GNU General Public License v3 (GPLv3)**.  
Original Spoolman integration code Copyright (C) 2023 Daniel Hultgren.
