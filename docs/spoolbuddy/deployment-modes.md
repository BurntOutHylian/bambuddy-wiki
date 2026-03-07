---
title: Deployment Modes
description: Choose between full local install or SpoolBuddy-only companion mode
---

# Deployment Modes

SpoolBuddy supports two recommended deployment models.

---

## :material-lan-connect: Mode A - Companion Only (Preferred for Lower-RAM Pi)

Run only SpoolBuddy on the Pi connected to the display; connect to remote Bambuddy server.

### When to choose this

- You already run Bambuddy on a NAS/server/mini-PC.
- You want kiosk hardware separated from core server.
- Your Pi is 2GB class and should not run full stack.

### Install command

```bash
sudo ./install.sh --mode spoolbuddy --bambuddy-url http://192.168.1.100:8000 --api-key bb_xxx --yes
```

### Notes

- Pi only runs kiosk + daemon + hardware interfaces.
- Remote Bambuddy handles API/database/web tasks.

---

## :material-server: Mode B - Full Local (Bambuddy + SpoolBuddy on the Same Pi)

Run both services on one Raspberry Pi:

- Bambuddy backend/frontend
- SpoolBuddy daemon
- local kiosk display session

### When to choose this

- You want an all-in-one box.
- Your Pi has enough resources for both workloads (4GB+ recommended).
- You prefer simpler network topology.

### Install command

```bash
sudo ./install.sh --mode full --port 8000 --yes
```

### Notes

- After first boot, create API key in Bambuddy and update `spoolbuddy/.env`.
- Good for single-printer or compact setups.

---

## :material-lightbulb: Recommendation

- For Pi 2GB class devices, use **Companion Only**.
- For Pi 4GB+ class devices, choose based on whether you want all-in-one or split architecture.
