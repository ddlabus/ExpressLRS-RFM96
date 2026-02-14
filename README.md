# ExpressLRS 4.0 for RFM96 (433MHz)

Custom ELRS RX firmware for RFM96 module (SX1276, +17dBm max).

## Hardware
- **RX:** ESP-01F (ESP8285) + RFM96

## Frequency
- Band: US433W (423.5-438MHz, 20 channels)

## Compatibility
Works with TX using E32-400M30S module (same band).

## Download
See [Releases](https://github.com/ddlabus/ExpressLRS-RFM96/releases) for compiled firmware.

## Files
| File | Description |
|------|-------------|
| `ELRS_4.0_RX_ESP8285_RFM96_US433W.bin` | Receiver firmware |
| `RFM96_RX.json` | RX hardware layout |

## Pinout (ESP-01F to RFM96)
| ESP-01F | RFM96 |
|---------|-------|
| GPIO4   | DIO0  |
| GPIO5   | DIO1  |
| GPIO12  | MISO  |
| GPIO13  | MOSI  |
| GPIO14  | SCK   |
| GPIO15  | NSS   |
| GPIO16  | LED   |

## Flashing
Use [esptool](https://github.com/espressif/esptool) or ELRS Configurator.
