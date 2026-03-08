---
title: SpoolBuddy
description: Optional Raspberry Pi add-on for NFC-based spool identification and management
---

# SpoolBuddy

SpoolBuddy is an optional companion hardware add-on that brings NFC-powered spool management to your Bambuddy setup. Using a Raspberry Pi and an NFC reader, you can tag your filament spools with NFC stickers and instantly identify them by tapping.

!!! info "Community project"
    SpoolBuddy documentation is being written by our contributors. Want to help? Join us on [Discord](https://discord.gg/aFS3ZfScHM)!

SpoolBuddy connects a Raspberry Pi with an NFC reader to your Bambuddy instance, enabling:

- **Instant spool identification** &mdash; Tap a spool to pull up its details.
- **NFC tag writing** &mdash; Write spool data to NFC stickers for easy tracking.
- **Inventory sync** &mdash; Spool data syncs with your Bambuddy inventory automatically.
- **Spool weight tracking** &mdash; Tracks live spool weight from the connected scale.
- **Fully local** &mdash; Runs entirely on your network, no cloud required.

---

## :material-rocket-launch: Getting Started

<div class="feature-grid" markdown>

<div class="feature-card" markdown>
### [:material-clipboard-list: Hardware Requirements](hardware.md)
What you need to build a current SpoolBuddy device &mdash; Raspberry Pi, touchscreen, PN5180 NFC reader, scale module, and wiring.
</div>

<div class="feature-card" markdown>
### [:material-format-list-checks: Materials Required](materials.md)
Practical bill of materials for a complete SpoolBuddy build.
</div>

<div class="feature-card" markdown>
### [:material-vector-polyline: Wiring Diagrams](wiring-diagrams.md)
Pin maps and ASCII wiring diagrams for PN5180 NFC and NAU7802 scale connections. *(Work in progress — community contributions welcome.)*
</div>

<div class="feature-card" markdown>
### [:material-download: Installation](installation.md)
Install the SpoolBuddy stack from the Bambuddy repository and enable kiosk auto-start on boot.
</div>

<div class="feature-card" markdown>
### [:material-lan-connect: Deployment Modes](deployment-modes.md)
Choose between all-in-one Pi setup (Bambuddy + SpoolBuddy) and companion-only mode.
</div>

<div class="feature-card" markdown>
### [:material-cog: Configuration](configuration.md)
Connect to Bambuddy, set API access, tune display/scale behavior, and verify NFC/tag workflows.
</div>

<div class="feature-card" markdown>
### [:material-raspberry-pi: Supported Pis](supported-pis.md)
Compatibility matrix and practical recommendations for Raspberry Pi models.
</div>

</div>
