# ExpressLRS RX for RFM96 (433MHz)

Custom ELRS RX firmware for RFM96 module (SX1276, +17dBm max).

![RFM96 Module](https://cdn-shop.adafruit.com/970x728/3073-00.jpg)

## Hardware

### Receiver (RX only)
- **MCU:** ESP-01F (ESP8285)
- **Radio:** RFM96 (SX1276, +17dBm)

![ESP-01F](https://www.cdebyte.com/u_file/2212/photo/4b67b3f116.png)

## Frequency
- Band: US433W (423.5-438MHz, 20 channels)

## Compatibility
Works with TX using **E32-400M30S** module (same band).

---

## Wiring Diagram

### RX: ESP-01F + RFM96

```
ESP-01F (ESP8285)          RFM96
┌─────────────────┐        ┌─────────────────┐
│ GPIO3 (RX) ─────┼────────┼─ (to FC)        │
│ GPIO1 (TX) ─────┼────────┼─ (from FC)      │
│ GPIO4  ─────────┼────────┼─ DIO0           │
│ GPIO5  ─────────┼────────┼─ DIO1           │
│ GPIO12 ─────────┼────────┼─ MISO           │
│ GPIO13 ─────────┼────────┼─ MOSI           │
│ GPIO14 ─────────┼────────┼─ SCK            │
│ GPIO15 ─────────┼────────┼─ NSS            │
│ GPIO16 ─────────┼────────┼─ LED (optional) │
│ 3V3    ─────────┼────────┼─ VCC (3.3V)     │
│ GND    ─────────┼────────┼─ GND            │
└─────────────────┘        └─────────────────┘
```

| ESP-01F Pin | RFM96 Pin | Function |
|-------------|-----------|----------|
| GPIO4 | DIO0 | Radio interrupt |
| GPIO5 | DIO1 | Radio interrupt |
| GPIO12 | MISO | SPI data in |
| GPIO13 | MOSI | SPI data out |
| GPIO14 | SCK | SPI clock |
| GPIO15 | NSS | SPI chip select |

**Note:** RFM96 has no external PA, so no RXEN/TXEN pins needed.

---

## Flashing Firmware on Virgin ESP

### Requirements
- USB-TTL adapter (CH340, CP2102, FT232)
- `pip install esptool`

### Wiring for flashing
```
USB-TTL          ESP-01F
─────────        ───────
TX      ──────── GPIO3 (RX)
RX      ──────── GPIO1 (TX)
3V3     ──────── VCC + CH_PD (EN)
GND     ──────── GND + GPIO0 + GPIO15
```

### Flash command
```bash
esptool.py --port /dev/ttyUSB0 --baud 460800 write_flash 0x0 ELRS_*_RX_ESP8285_RFM96_US433W.bin
```

### After Flashing
1. Disconnect GPIO0 from GND, power cycle
2. Connect to WiFi: `ExpressLRS RX`
3. Configure at `10.0.0.1`

---

## Download
See [Releases](https://github.com/ddlabus/ExpressLRS-RFM96/releases)

## Links
- [RFM96 Datasheet](https://www.hoperf.com/modules/lora/RFM96.html)
- [ExpressLRS Documentation](https://www.expresslrs.org/)
