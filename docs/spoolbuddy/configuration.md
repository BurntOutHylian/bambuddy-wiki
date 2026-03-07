---
title: Configuration
description: Connecting SpoolBuddy to your Bambuddy instance
---

# Configuration

This page covers the runtime settings used by the SpoolBuddy daemon and kiosk.

---

## :material-key: Backend Connection

SpoolBuddy daemon reads its connection settings from:

- `/opt/bambuddy/spoolbuddy/.env` (default install path)

Minimum configuration:

```bash
SPOOLBUDDY_BACKEND_URL=http://192.168.1.100:8000
SPOOLBUDDY_API_KEY=bb_xxx
```

Optional:

```bash
SPOOLBUDDY_DEVICE_ID=sb-yourfixedid
SPOOLBUDDY_HOSTNAME=spoolbuddy-pi
```

After changes:

```bash
sudo systemctl restart spoolbuddy
```

!!! tip "API key source"
    Create API keys in **Bambuddy → Settings → API Keys**.

---

## :material-monitor-dashboard: Kiosk Access and Auth

The kiosk runs at:

- `/spoolbuddy`

Installer-generated kiosk URL usually includes a token:

- `/spoolbuddy?token=bb_xxx`

On first load, Bambuddy stores that token and removes it from the visible URL.

---

## :material-nfc: NFC Behavior

SpoolBuddy supports:

- **Bambu RFID tags** (MIFARE Classic; reads tray/material metadata)
- **NTAG tags** (`NTAG213/215/216`) for writable custom tags

### Tag Writing

Tag writing is available in kiosk UI at:

- `/spoolbuddy/write-tag`

Current write format:

- OpenTag3D-compatible NDEF payload (`application/opentag3d`)

---

## :material-scale: Scale and Calibration

Scale settings are managed from kiosk **Settings**:

- `Scale` tab for tare/calibration
- `Display` tab for brightness + blank timeout

Calibration flow:

1. Remove all weight and run **Set Zero / Tare**
2. Place known reference weight
3. Run **Calibrate**

Daemon receives and applies calibration via heartbeat, then persists through Bambuddy.

!!! tip "No calibration weight available? Use coins with known weight"
    If you do not have a calibration weight, coins are a practical fallback.
    Example euro coin weights:
    - `€2` = `8.50 g`
    - `€1` = `7.50 g`
    - `50 cent` = `7.80 g`
    - `20 cent` = `5.74 g`
    Use clean, undamaged coins and enter the exact total grams of the coin stack you place on the scale.

---

## :material-sync: Device Sync Model

The daemon:

- registers device capabilities (NFC, scale, backlight)
- sends heartbeat periodically
- pushes tag scans and scale readings
- receives pending commands (for example `tare`, `write_tag`)

If heartbeat stops, device is marked offline after timeout.

### AMS Behavior Clarification

SpoolBuddy does **not** physically switch spools.  
It configures AMS slots with filament/K-profile information and works with Bambuddy's AMS/inventory workflows.

---

## :material-update: Updating

For normal Pi updates, a full reinstall is usually not required.

Typical flow:

```bash
git pull
sudo systemctl restart spoolbuddy
```

If your local checkout is outdated, update it first, then run the same restart.

---

## :material-database-import: Spoolman Import (Optional)

If you already have data in Spoolman, Bambuddy includes an import script:

```bash
# Preview
python scripts/import_spoolman.py --spoolman-url http://localhost:7912/ --bambuddy-url http://localhost:8000/ --dry-run

# Import
python scripts/import_spoolman.py --spoolman-url http://localhost:7912/ --bambuddy-url http://localhost:8000/

# With API key and archived spools
python scripts/import_spoolman.py --spoolman-url http://localhost:7912/ --bambuddy-url http://localhost:8000/ --api-key YOUR_KEY --archived
```

---

## :material-alert: Troubleshooting

### Device stays offline

- Verify `SPOOLBUDDY_BACKEND_URL` and `SPOOLBUDDY_API_KEY`.
- Check service logs:

```bash
sudo journalctl -u spoolbuddy -f
```

### NFC not detected

- Confirm PN5180 wiring and SPI enablement
- Confirm `dtoverlay=spi0-0cs`.
- Run:

```bash
sudo /opt/bambuddy/spoolbuddy/venv/bin/python /opt/bambuddy/spoolbuddy/scripts/pn5180_diag.py
```

### Scale shows no readings

- Confirm NAU7802 on I2C bus 0:

```bash
sudo i2cdetect -y 0
```

- Run:

```bash
sudo /opt/bambuddy/spoolbuddy/venv/bin/python /opt/bambuddy/spoolbuddy/scripts/scale_diag.py
```

### Scale calibration is inconsistent

- Ensure the RFID reader is not mechanically/electrically interfering with the scale platform.
- If needed, relocate RFID placement away from the weigh path and recalibrate.

### Brightness controls do nothing

- HDMI displays are dimmed by frontend CSS
- Physical backlight writes require a DSI backlight device and `video` group permissions

### Display goes blank when connecting touch

- This can indicate display-side power/ground issues (for example ground loop-like behavior).
- Test with a different Pi/power source and re-check cabling and adapter orientation.
