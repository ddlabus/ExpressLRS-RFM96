# ExpressLRS RX for RFM96 (433MHz)

Custom ELRS RX firmware for RFM96 module (SX1276, +17dBm max).

![RFM96 Module](https://raw.githubusercontent.com/ddlabus/ExpressLRS-RFM96/main/images/RFM96.avif)

## Hardware

### Receiver (RX only)
- **MCU:** ESP32-C3 SuperMini
- **Radio:** RFM96 (SX1276, +17dBm)

![ESP32-C3 SuperMini](https://raw.githubusercontent.com/ddlabus/ExpressLRS-RFM96/main/images/ESP32-C3.avif)

## Frequency
- Band: US433W (423.5-438MHz, 20 channels)

## Compatibility
Works with TX using **E32-400M30S** module (same band).

---

## Wiring Diagram

### RX: ESP32-C3 SuperMini + RFM96

```
ESP32-C3 SuperMini         RFM96
┌─────────────────┐        ┌─────────────────┐
│                 │        │                 │
│ GPIO20 (RX) ────┼────────┼─ (to FC)        │
│ GPIO21 (TX) ────┼────────┼─ (from FC)      │
│                 │        │                 │
│ GPIO1  ─────────┼────────┼─ DIO0           │
│ GPIO2  ─────────┼────────┼─ DIO1           │
│ GPIO5  ─────────┼────────┼─ MISO           │
│ GPIO4  ─────────┼────────┼─ MOSI           │
│ GPIO6  ─────────┼────────┼─ SCK            │
│ GPIO7  ─────────┼────────┼─ NSS            │
│ GPIO3  ─────────┼────────┼─ RST            │
│                 │        │                 │
│ GPIO8  ─────────┼────────┼─ LED            │
│                 │        │                 │
│ 3V3    ─────────┼────────┼─ VCC (3.3V)     │
│ GND    ─────────┼────────┼─ GND            │
└─────────────────┘        └─────────────────┘
```

| ESP32-C3 Pin | RFM96 Pin | Function |
|--------------|-----------|----------|
| GPIO20 | - | Serial RX (to FC) |
| GPIO21 | - | Serial TX (from FC) |
| GPIO1 | DIO0 | Radio interrupt |
| GPIO2 | DIO1 | Radio interrupt |
| GPIO5 | MISO | SPI data in |
| GPIO4 | MOSI | SPI data out |
| GPIO6 | SCK | SPI clock |
| GPIO7 | NSS | SPI chip select |
| GPIO3 | RST | Radio reset |
| GPIO8 | - | LED |
| 3V3 | VCC | Power 3.3V |
| GND | GND | Ground |

**Note:** RFM96 has no external PA, so no RXEN/TXEN pins needed.

---

## Flashing Firmware

### RX (ESP32-C3 SuperMini)

**Via USB-C (built-in bootloader):**
1. Hold BOOT button
2. Connect USB-C cable
3. Release BOOT button

```bash
esptool.py --port /dev/ttyACM0 --baud 460800 \
    --chip esp32c3 write_flash 0x0 ELRS_*_RX_ESP32C3_RFM96_US433W.bin
```

### After Flashing
1. Power cycle the module
2. Connect to WiFi: `ExpressLRS RX`
3. Configure at `10.0.0.1`

---

## Download
See [Releases](https://github.com/ddlabus/ExpressLRS-RFM96/releases)

## Files
| File | Description |
|------|-------------|
| `ELRS_*_RX_ESP32C3_RFM96_US433W.bin` | Receiver firmware (ESP32-C3) |
| `ESP32C3_SuperMini_RX.json` | RX hardware layout |

## Links
- [RFM96 Datasheet](https://www.hoperf.com/modules/lora/RFM96.html)
- [ESP32-C3 SuperMini](https://www.aliexpress.com/item/1005005967641936.html)
- [ExpressLRS Documentation](https://www.expresslrs.org/)
