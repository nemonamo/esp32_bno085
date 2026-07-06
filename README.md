<h1 align="center">ESP32 BNO085</h1>

<p align="center">
  <strong>A compact ESP32-S3 + BNO085 KiCad hardware design for 9-axis motion sensing.</strong>
</p>

<p align="center">
  <img alt="KiCad" src="https://img.shields.io/badge/KiCad-hardware%20design-314cb0">
  <img alt="MCU" src="https://img.shields.io/badge/MCU-ESP32--S3-orange">
  <img alt="Sensor" src="https://img.shields.io/badge/IMU-BNO085-16a34a">
  <img alt="License" src="https://img.shields.io/badge/license-not%20declared-lightgrey">
</p>

<p align="center">
  <a href="#features">Features</a> |
  <a href="#repository-contents">Contents</a> |
  <a href="#open-the-project">Open</a> |
  <a href="#fabrication-checklist">Fabrication</a> |
  <a href="#license">License</a>
</p>

This repository contains the KiCad design files for a small ESP32-S3 board built around the BNO085 9-axis smart IMU. It is meant as a hardware design workspace: schematic, PCB layout, footprint libraries, and fabrication-toolkit settings are tracked, while generated Gerbers and local analysis outputs stay out of Git.

## Features

- **ESP32-S3 module** - Wi-Fi/BLE capable MCU module footprint in the schematic and PCB.
- **BNO085 smart IMU** - accelerometer, gyroscope, magnetometer, and sensor-fusion capable motion sensor.
- **USB-C interface** - USB 2.0 Type-C receptacle for board connectivity.
- **Local footprints included** - custom BNO085 and Molex connector footprint libraries are checked in.
- **Fabrication-toolkit settings** - export options are versioned for repeatable manufacturing output.

## Repository Contents

```text
esp32_bno085.kicad_pro          KiCad project file
esp32_bno085.kicad_sch          Schematic
esp32_bno085.kicad_pcb          PCB layout
fp-lib-table                    Local footprint library table
BNO085.pretty/                  BNO085 footprint
530480210.pretty/               Molex connector footprint
fabrication-toolkit-options.json
```

Generated files are intentionally excluded:

```text
analysis/
production/
*-backups/
.history/
*.kicad_prl
```

## Open the Project

1. Install KiCad 8 or newer.
2. Clone this repository.
3. Open `esp32_bno085.kicad_pro` in KiCad.
4. Confirm the local footprint libraries resolve from `fp-lib-table`.
5. Run ERC and DRC before exporting fabrication files.

```powershell
git clone https://github.com/nemonamo/esp32_bno085.git
cd esp32_bno085
```

## Fabrication Checklist

Before ordering boards:

- Run KiCad ERC on `esp32_bno085.kicad_sch`.
- Run KiCad DRC on `esp32_bno085.kicad_pcb`.
- Re-export Gerbers, drill files, BOM, and CPL from the current board.
- Review USB D+/D- clearance and connector orientation.
- Review BNO085 I2C pull-ups and power rails.
- Confirm the fabrication house design rules match the current PCB constraints.

The previous board review focused on JLCPCB-relevant copper geometry issues, small vias, USB D- clearance, silkscreen/text warnings, and BNO085 environmental I2C pull-ups. Re-run checks after every layout change.

## What This Repo Is Not

- No firmware is included.
- No generated production package is included.
- No guarantee is made that the latest commit has been fabricated exactly as-is.

## Security and Safety

Hardware repositories can still leak private information through generated archives, supplier exports, order files, screenshots, or local notes. Keep production exports and analysis reports local unless they have been reviewed.

## License

No open-source hardware or software license is currently declared. Add a `LICENSE` file before publishing this design for reuse, fabrication by others, or external contribution.
