# ESP32 BNO085

KiCad project for an ESP32-based BNO085 board.

## Contents

- `esp32_bno085.kicad_pro` - KiCad project
- `esp32_bno085.kicad_sch` - schematic
- `esp32_bno085.kicad_pcb` - PCB layout
- `fabrication-toolkit-options.json` - fabrication toolkit settings

Generated analysis files, local backups, and previous fabrication outputs are intentionally excluded from this repository.

## Fabrication Notes

The latest board review fixed JLCPCB-relevant copper geometry issues, including small vias, USB D- clearance, silkscreen/text warnings, and missing BNO085 environmental I2C pull-ups.

Before ordering, rerun KiCad DRC/ERC and export fresh Gerbers, BOM, and CPL from the current KiCad project.
