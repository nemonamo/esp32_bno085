<h1 align="center">ESP32 BNO085</h1>

<p align="center">
  <strong>A compact ESP32-S3 + BNO085 KiCad hardware design for 9-axis motion sensing.</strong>
</p>

<p align="center">
  <a href="../../README.md">한국어</a> |
  English |
  <a href="README.zh-CN.md">中文</a> |
  <a href="README.ja.md">日本語</a>
</p>

This repository contains the KiCad design files for a small ESP32-S3 board built around the BNO085 9-axis smart IMU. Schematic, PCB layout, footprint libraries, and fabrication-toolkit settings are tracked; generated Gerbers and local analysis outputs are excluded.

## Features

- **ESP32-S3 module** - Wi-Fi/BLE capable MCU module footprint.
- **BNO085 smart IMU** - accelerometer, gyroscope, magnetometer, and sensor-fusion capable sensor.
- **USB-C interface** - USB 2.0 Type-C receptacle.
- **Local footprints included** - BNO085 and Molex connector footprint libraries.
- **Fabrication-toolkit settings** - export options for repeatable manufacturing output.

## Repository Contents

```text
esp32_bno085.kicad_pro
esp32_bno085.kicad_sch
esp32_bno085.kicad_pcb
fp-lib-table
BNO085.pretty/
530480210.pretty/
fabrication-toolkit-options.json
```

## Open the Project

```powershell
git clone https://github.com/nemonamo/esp32_bno085.git
cd esp32_bno085
```

Open `esp32_bno085.kicad_pro` in KiCad 8 or newer, confirm local footprints resolve, then run ERC and DRC before exporting fabrication files.

## Fabrication Checklist

- Run KiCad ERC and DRC.
- Re-export Gerbers, drill files, BOM, and CPL.
- Review USB D+/D- clearance and connector orientation.
- Review BNO085 I2C pull-ups and power rails.
- Confirm fabrication-house design rules.

## Security and Safety

Keep generated archives, order files, supplier exports, screenshots, and local notes out of Git unless they have been reviewed.

## License

No open-source hardware or software license is currently declared. Add a `LICENSE` file before publishing this design for reuse, fabrication by others, or external contribution.
