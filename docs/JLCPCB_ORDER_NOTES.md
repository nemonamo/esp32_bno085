# JLCPCB Order Notes

Last checked: 2026-07-13

Detailed current-state review: [`VERIFICATION_REPORT.md`](VERIFICATION_REPORT.md)

This board keeps the existing outline. Do not enlarge the PCB only to satisfy
assembly handling requirements. If JLCPCB asks for handling area, use a panel,
mouse bites, V-cut, or edge rails around the board.

## Current KiCad Checks

- KiCad 10 ERC: 0 violations.
- KiCad 10 PCB DRC with schematic parity: 0 violations, 0 unconnected items,
  0 schematic parity issues.
- If every project-ignored PCB check is temporarily enabled, the remaining
  warnings are footprint-library comparison warnings (`lib_footprint_mismatch`).
  They indicate that the board-embedded footprint copies differ from the
  currently installed KiCad library versions. They are not clearance,
  unconnected-net, or schematic-parity failures.
- R10/R11 now include B.CrtYd courtyard outlines, so they no longer trigger
  `missing_courtyard` when that normally ignored check is enabled.
- Board outline from the PCB file is about 24.5 mm x 53.4 mm.

## JLCPCB Assembly Constraints

- The PCB has SMD components on both F.Cu and B.Cu.
- Economic PCBA is single-sided placement. Use Standard PCBA for double-sided
  assembly, or move the assembled parts to one side before using Economic PCBA.
- Standard PCBA currently has a 70 mm x 70 mm minimum single-PCB/panel handling
  size. Keep the board outline unchanged and use a panel/rails if required.
- JLCPCB marks fiducials as necessary for Standard PCBA, but their assembly FAQ
  says customers do not have to add fiducial marks themselves because JLCPCB can
  add them for SMT assembly. Prefer panel/rail fiducials over forcing them into
  this compact board.

## Geometry Notes

- Current project rules use 0.1016 mm minimum track width/clearance.
- JLCPCB's current 1 oz 1/2-layer capability lists 0.10 mm / 0.10 mm minimum
  track width/spacing, so the 0.1016 mm routes are inside that published limit.
- Current default vias are 0.5 mm diameter / 0.3 mm drill. JLCPCB lists
  0.25 mm diameter / 0.15 mm hole as the minimum via capability, with 0.2 mm
  hole preferred, so these vias are not the limiting geometry.
- The USB-C and battery connector footprints intentionally extend to the board
  edge. Some generic DFM analyzers report this as an edge-clearance error, but
  it is not a KiCad DRC violation.

## Via-In-Pad Note

There is a via at/near the D2 pad area. For assembled boards, ask JLCPCB for
epoxy-filled and capped or copper-filled and capped vias where needed, or
review the solder-wicking risk in the assembly preview. JLCPCB notes that vias
in pads cannot be plugged with ink and should use epoxy or copper filling when
that finish is required.

## BOM/CPL Handoff

- BOM and CPL are intentionally not generated in this repository state.
- KiCad `MPN`, `Manufacturer`, and `LCSC` fields are populated for seven
  non-generic/order-critical lines: D1, J1, J2, Q1, U1, U3, and U4.
- The exact ESP32-S3 module variant is still intentionally unset. Choose the
  actual flash/PSRAM variant, such as an N8R8 or N16R8 orderable module, before
  filling U2.
- Passives, LEDs, switches, and the 32.768 kHz crystal still need exact
  JLCPCB/LCSC choices for value, tolerance, voltage rating, dielectric, color,
  height, actuator, and load-capacitance details.
- Before ordering assembly, fill exact LCSC part numbers and verify all part
  rotations in the JLCPCB preview, especially USB-C, SOT-23/SOT-23-5, SOIC-8,
  LEDs, and diodes.
- U3 BNO085 has a BOM note because the LCSC page showed it out of stock on
  2026-07-13. Verify JLCPCB availability or pre-order status before PCBA.
- J1 is a through-hole battery header. Confirm Standard PCBA support for that
  line or plan to hand-solder/consign it.
- The current design does not include a USB ESD/EMC filter near J2. This does
  not fail KiCad DRC, but it is still a robustness/EMC tradeoff for production.

## Official References

- PCB capabilities: https://jlcpcb.com/capabilities/pcb-capabilities
- PCBA capabilities: https://jlcpcb.com/capabilities/pcb-assembly-capabilities
- Assembly FAQ: https://jlcpcb.com/help/article/pcb-assembly-faqs
- Via covering: https://jlcpcb.com/help/article/pcb-via-covering
