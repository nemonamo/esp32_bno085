# Verification Report

Last checked: 2026-07-13  
Commit checked: `34df731`

This report is a current-state review, not a blanket guarantee. The board passes
KiCad ERC/DRC, and the main power, USB boot, reset/boot button, and BNO085 mode
connections are internally consistent. It is not fully order-ready for assembled
JLCPCB production until the BOM/LCSC part numbers and placement preview are
completed.

## Checks Run

- KiCad 10 schematic ERC: 0 violations.
- KiCad 10 PCB DRC with zone refill and schematic parity: 0 violations,
  0 unconnected items, 0 schematic parity issues.
- KiCad DRC with all project-ignored checks temporarily enabled:
  32 `lib_footprint_mismatch` warnings only.
- Schematic analyzer: 30 findings.
- PCB analyzer with full coordinate/proximity data: 58 findings.
- Schematic/PCB cross-analysis: 1 finding.
- EMC analyzer: 20 findings, score 31/100.
- Thermal analyzer at 40 C ambient: 0 findings, score 100/100.
- Gerber/drill export and Gerber analyzer: 3 warnings.

Generated outputs are under `analysis/review_20260713/34df731/`.

## Critical Bring-Up Checks

### ESP32-S3 USB and Boot

- USB-C VBUS pins A4/A9/B4/B9 connect to `+5V`.
- USB-C D+ pins A6/B6 connect to `USB_D+`.
- USB-C D- pins A7/B7 connect to `USB_D-`.
- ESP32-S3-WROOM-1 pad 14 connects to `USB_D+`.
- ESP32-S3-WROOM-1 pad 13 connects to `USB_D-`.
- CC1 and CC2 each have 5.1k pull-down resistors to GND.
- `SW1 RESET` shorts `ESP_EN` to GND. `ESP_EN` has a 10k pull-up to +3.3V.
- `SW2 BOOT` shorts `BOOT`/GPIO0 to GND.

Conclusion: USB enumeration failure is not explained by missing reset/setup
buttons. The board has both RESET and BOOT buttons, and the USB-C device-side
CC and D+/D- wiring matches the ESP32-S3 native USB pins.

Relevant Espressif references:

- ESP32-S3-WROOM-1 datasheet:
  https://documentation.espressif.com/esp32-s3-wroom-1_wroom-1u_datasheet_en.pdf
- ESP32-S3 hardware design checklist:
  https://docs.espressif.com/projects/esp-hardware-design-guidelines/en/latest/esp32s3/schematic-checklist.html

### Power Tree

- USB `+5V` feeds `VSYS` through D1.
- Battery connector J1 pin 1 feeds `BAT`.
- Battery charger U1 BAT pin is on `BAT`.
- P-channel MOSFET Q1 uses pin 1 gate on `+5V`, pin 2 source on `BAT`,
  and pin 3 drain on `VSYS`.
- R3 pulls the `+5V`/Q1-gate node to GND when USB is absent, enabling battery
  power to `VSYS`.
- U4 XC6220B331MR has VIN and CE on `VSYS`, GND on GND, and VOUT on `+3.3V`.

Conclusion: The schematic/PCB power path is coherent for USB-powered `VSYS`
and battery-powered `VSYS`. A board that does not power up should be checked
physically at these points in order: USB VBUS, `VSYS`, U4 VOUT `+3.3V`,
ESP32 `EN`.

KiCad ERC also confirms the power source declarations are valid. The existing
PWR_FLAG symbols on the `+5V` and `VSYS` rails are sufficient; adding duplicate
PWR_FLAGs on those same rails creates a power-output-to-power-output ERC error.

Relevant component references:

- XC6220 datasheet:
  https://product.torexsemi.com/system/files/series/xc6220.pdf
- AO3401A datasheet:
  https://www.aosmd.com/res/data_sheets/AO3401A.pdf

### BNO085 Mode and Clock

- BNO085 VDD and VDDIO are on `+3.3V`.
- BNO085 PS1 is tied to `+3.3V`.
- BNO085 PS0/WAKE is tied to GND.
- BNO085 BOOTN is tied high.
- BNO085 XOUT32/CLKSEL1 and XIN32 connect to Y1 with C8/C9 load capacitors.
- BNO085 UART pins connect crosswise:
  `ESP_TX/BNO_RX` to BNO085 pin 19, and `ESP_RX/BNO_TX` to BNO085 pin 20.

Conclusion: The BNO085 is strapped for UART-SHTP mode and has the external
32.768 kHz crystal required for reliable UART operation. BOOTN is tied directly
high; the datasheet recommends a 10k pull-up and optional MCU GPIO for DFU, so
direct high is a robustness/DFU tradeoff rather than a likely power-up blocker.

Relevant CEVA reference:

- BNO08X datasheet:
  https://www.ceva-ip.com/wp-content/uploads/BNO080_085-Datasheet.pdf

## JLCPCB Status

Current board outline is about 24.5 mm x 53.4 mm. Do not enlarge the board
outline for assembly handling. If JLCPCB requires handling area, use a panel,
mouse bites, V-cut, or edge rails around the unchanged board outline.

Current board geometry against JLCPCB published limits:

- Minimum routed signal width is about 0.1016 mm. JLCPCB lists 0.10/0.10 mm
  minimum track width/spacing for 1 oz 1- and 2-layer boards.
- Vias are 0.5 mm diameter / 0.3 mm drill. JLCPCB lists 0.25 mm diameter /
  0.15 mm hole as the 2-layer minimum, with 0.2 mm hole preferred.
- The board has SMD components on both F.Cu and B.Cu. Use Standard PCBA for
  double-sided assembly, or move assembled parts to one side before Economic
  PCBA.
- Standard PCBA requires handling/fiducials, but JLCPCB's assembly FAQ says
  they can add fiducial marks for SMT assembly. Prefer panel/rail fiducials
  instead of changing this compact board outline.

Relevant JLCPCB references:

- PCB capabilities:
  https://jlcpcb.com/capabilities/pcb-capabilities
- PCBA capabilities:
  https://jlcpcb.com/capabilities/pcb-assembly-capabilities
- Assembly FAQ:
  https://jlcpcb.com/help/article/pcb-assembly-faqs
- Via covering:
  https://jlcpcb.com/help/article/pcb-via-covering

## Remaining Issues Before Ordering

| Item | Severity | Status |
| --- | --- | --- |
| BOM/LCSC/MPN coverage | Blocker for assembled order | Current schematic has 0/24 unique BOM parts with MPN fields populated. User-owned BOM/CPL step must fill exact JLCPCB/LCSC parts. |
| CPL rotation preview | Blocker for assembled order | Must be checked in JLCPCB preview, especially USB-C, BNO085 LGA, SOT-23, SOT-23-5, SOIC-8, diodes, and LEDs. |
| Standard PCBA handling | Order setup | Board is smaller than Standard PCBA handling size by itself. Use JLCPCB panel/rails; do not alter outline. |
| Via-in-pad / solder wicking | Order setup | Analyzer reports an untented via at/near D2 pad 1. Use JLCPCB via covering/filled-and-capped option where needed, or inspect the assembly preview carefully. |
| USB ESD/filtering | Robustness risk | No USB ESD array or reserved 22/33 ohm series resistor footprints. Espressif recommends reserving USB series resistors and optional capacitors near the chip. This is not a KiCad DRC failure. |
| USB routing symmetry | Robustness risk | Cross-analysis reports USB D+/D- via/layer asymmetry. Full-speed USB is tolerant, but this remains an EMC/SI weakness. |
| EMC score | Robustness risk | EMC analyzer score is 31/100, mostly from no USB filtering, 2-layer adjacent signal layers, USB layer changes, and edge-near sensitive nets. |
| Physical bring-up | Not tested | No measurement evidence yet. Check USB VBUS, `VSYS`, `+3.3V`, `ESP_EN`, and USB D+/D- continuity on a real board. |
| SPICE simulation | Not run | No SPICE simulator was installed in this environment. |
| Lifecycle audit | Not meaningful yet | MPN/LCSC fields are not populated, so lifecycle/stock audit cannot prove availability. |

## Analyzer False Positives or Non-Blockers

- Remaining all-check DRC warnings are `lib_footprint_mismatch`. These mean the
  board-embedded footprint copies differ from the currently installed KiCad
  library versions. They are not clearance, unconnected-net, or schematic-parity
  failures.
- Schematic analyzer `RS-001` warnings on `+5V` and `VSYS` are not KiCad ERC
  failures. Raw ERC testing shows those rails already have PWR_FLAG source
  declarations; duplicating them causes an ERC error.
- `PM-002` on J1/J2 edge distance is expected for edge/overhanging connectors.
- `FD-001` no fiducials is a JLCPCB assembly setup issue, not an electrical
  failure. Use panel/rail fiducials if needed.
- Gerber paste-to-copper ratio warnings are expected because paste layers only
  contain SMD paste apertures, not all copper features.

## Practical Bring-Up Checklist

1. Plug in USB-C and measure J2 VBUS to GND: about 5 V expected.
2. Measure `VSYS`: USB input should appear through D1.
3. Measure U4 VOUT / `+3.3V`: about 3.3 V expected.
4. Measure ESP32 `EN`: normally high, low only while RESET is pressed.
5. Hold BOOT, tap RESET, release RESET, then release BOOT to enter download
   mode.
6. Check USB D+ and D- continuity from J2 to U2 pads 14 and 13.
7. If the PC still does not enumerate, inspect soldering on J2, U2 pins 13/14,
   D1, U4, and the GND shield/pads before changing the schematic.
