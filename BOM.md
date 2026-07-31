# Bill of Materials: Doorbell & Weather Wall Display

Companion to [`PRD.md`](PRD.md). Prices are July-2026 USD street prices researched online; items marked **⚠ verify** had volatile or unconfirmable pricing and must be re-checked in a live cart before quoting the client. Excludes the client's existing Ring doorbell and any Ring subscription.

Buy **Table A + Table B + Table D** for the recommended tablet build. Table C replaces Table A only if the client chooses the ESP32-P4 alternate (PRD §7).

## Table A — Primary display: Android tablet

| Item | Qty | Unit price | Ext. | Source | Notes |
|---|---|---|---|---|---|
| Amazon Fire HD 10 (32 GB) | 1 | $100–140 | $100–140 | Amazon | Cheapest. Fire OS caveats: Fully Kiosk sideloaded via APK, lockscreen ads unless removed, no Google Play. ⚠ verify sale pricing |
| — *or* — Samsung Galaxy Tab A9+ 11" | (1) | $130–200 | — | Amazon/Best Buy | Cleaner Android, Play Store, security patches into late 2027. Preferred if budget allows (PRD OQ-4) |
| Fully Kiosk Browser PLUS license | 1 | ~$9 | $9 | fully-kiosk.com | One-time, per device. Required for remote admin + HA integration |
| Tablet wall mount | 1 | $15–60 | $15–60 | VidaBox / Amazon / 3D print | 3D-printed frameless mounts: $0–15 filament (free STLs exist for Fire HD 10) |
| Smart plug (charge cycling) | 1 | $10–15 | $10–15 | Amazon (Kasa/similar) | Drives the 40–80% battery automation (PRD NFR-4) — battery-swelling mitigation |
| USB-C PSU + long cable | 1 | ~$15 | $15 | Amazon | Route inside wall or cable channel per mount choice |
| **Subtotal (Fire HD 10 build)** | | | **~$150–240** | | |

## Table B — Presence node (required in every configuration)

| Item | Qty | Unit price | Ext. | Source | Notes |
|---|---|---|---|---|---|
| HLK-LD2410C 24 GHz mmWave module | 1 | $5–12 | $5–12 | AliExpress / Amazon | Native ESPHome `ld2410` support. ⚠ verify — Amazon markup varies. LD2450 ($8–15) is an alt if multi-target zones ever needed |
| ESP32 dev board (nodemcu-32s / esp32dev) | 1 | $5–10 | $5–10 | AliExpress / Amazon | Matches existing fleet in this repo; flashed with [`presence-node.yaml`](presence-node.yaml) |
| Small project box + dupont wiring | 1 | ~$10 | $10 | Amazon / 3D print | Mount near display, sensor face unobstructed |
| **Subtotal** | | | **~$20–32** | | |

## Table C — Alternate display: ESP32-P4 custom build (replaces Table A; PRD §7)

| Item | Qty | Unit price | Ext. | Source | Notes |
|---|---|---|---|---|---|
| Guition JC1060P470 7" 1024×600 MIPI-DSI touch (ESP32-P4, 32 MB PSRAM, C6 Wi-Fi) | 1 | $34–42 | $34–42 | AliExpress | Strongest ESPHome/P4 community track record. ⚠ verify |
| — *or* — Guition JC8012P4A1 10.1" 800×1280 | (1) | $52–75 | — | AliExpress / eBay | Portrait-native panel used rotated; less prior art. ⚠ verify |
| 5 V/3 A USB-C PSU | 1 | $8–15 | $8–15 | Amazon | Size for full-backlight draw |
| Enclosure | 1 | $0–25 | $0–25 | 3D print | No off-the-shelf enclosure known for this board — custom print required (flagged effort) |
| Wiring (LD2410 can wire directly to this board's UART header — Table B ESP32 not needed) | 1 | ~$5 | $5 | — | Saves the separate node in this configuration |
| **Subtotal** | | | **~$47–87** | | **Plus Phase-2 firmware development labor (PRD §7) — order of weeks; not a materials cost** |
| *Upgrade option:* PoE Android in-wall panel 10.1" (e.g. JEESTON RK3576/Android 14) | (1) | ~$150–350 | — | Amazon / AliExpress | ⚠ verify + vet vendor. Batteryless, auto-boot on power restore, flush 86-box mount, Ethernet/PoE. Runs the same tablet software stack — eliminates consumer-tablet failure modes (PRD §7) |

## Table D — Hub & infrastructure (required in every configuration)

| Item | Qty | Unit price | Ext. | Source | Notes |
|---|---|---|---|---|---|
| Home Assistant Green | 1 | $199 | $199 | Nabu Casa / resellers | Official turnkey hub. Price raised from $99 to $199 in Jan 2026 (RAM shortage) — quote accordingly |
| — *or* — Raspberry Pi 5 (8 GB) + PSU + case + SD/NVMe | (1) | ~$125 + $40–60 | — | rpilocator | Pi prices inflated in 2026; HA Green is simpler to hand to a client |
| Home Assistant OS, Mosquitto, ring-mqtt, go2rtc | — | $0 | $0 | open source | Software stack (PRD §8) |
| Met.no or NWS weather | — | $0 | $0 | — | No API key (Met.no) / free US government API (NWS) |
| Fully Kiosk HA integration, `kiosk-mode` plugin | — | $0 | $0 | HA / HACS | |
| Ethernet cable to router | 1 | ~$8 | $8 | Amazon | Wire the hub; only the displays are Wi-Fi |
| **Subtotal** | | | **~$207** | | |

## Configuration totals

| Configuration | Materials total | Notes |
|---|---|---|
| **Recommended: tablet build** (A + B + D) | **~$380–480** | No firmware development; all future changes server-side |
| ESP32-P4 alternate (B-partial + C + D) | ~$260–330 | Plus substantial Phase-2 firmware labor; video limited to ~10–15 fps MJPEG |
| PoE panel upgrade (C-upgrade + B + D) | ~$380–590 ⚠ | Best longevity/aesthetics; pricing unverified |

**Recurring costs: none required.** Ring subscription optional (event playback only). Fully PLUS is one-time. Weather APIs are free.
