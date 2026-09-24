# uaEFI dual AMPSEAL 35-pin harness pinout

Light-touch redesign of the external harness connectors on this fork (`uaefi` rev E schematic/PCB). Electrical function of the rev E nets is preserved. Copper is **not** re-routed.

## What changed

| Before (rev E harness) | Pins | After |
| --- | ---: | --- |
| J2 Molex Mini-Fit Jr 5569-20A2 | 20 | Folded into J31 |
| J3 Molex Mini-Fit Jr 5569-06A2 (WBO) | 6 | Folded into J30 |
| J4 Molex Mini-Fit Jr 5569-08A2 (power / DC) | 8 | Folded into J30 |
| J5 Molex Mini-Fit Jr 5569-18A2 (inj / ign / LS) | 18 | Folded into J30 |
| J10 Molex Mini-Fit Jr 5569-16A2 (sensors / CAN) | 16 | Folded into J31 |
| **Total harness pins** | **68** | **J30 + J31 = 70** |

Those five Mini-Fit symbols are marked DNP / not on board. Their footprints were removed from `uaefi.kicad_pcb`. Stale tracks that used to land on those pads were left in place.

## Connectors

| Ref | Role | PCB header (hypothesis) | Mating plug |
| --- | --- | --- | --- |
| J30 | Connector A — power, injectors, ignition, low-side, DC motor, wideband | TE **776163-1** (35 pos, right angle, key/color 1, tin). Gold-plated equivalent is **1-776163-1**. | TE **776164-1** housing (35 pos, key 1) with terminal 770520 (reel) or 770854 (loose piece), per TE drawing 776163 note 5. |
| J31 | Connector B — sensor power, CAN, analog / digital inputs, VR, EGT | Same header family, second key if a keyed pair is required (776163-2 natural, -4 gray, -5 blue). This pass uses the same footprint for both. | Matching 776164-x plug. |

**776164-1 is the wire plug, not a PCB header.** Both board connectors are 776163-style headers.

### Footprint hypothesis

No AMPSEAL footprint existed in this repo, `kicad6-libraries/`, or `hellen-one/`. `footprints/TE_AMPSEAL_35_776163-1.kicad_mod` is adapted from the abandoned public KiCad footprint proposal [KiCad/kicad-footprints#633](https://github.com/KiCad/kicad-footprints/pull/633) (`TE_x-776163-x`), which cites TE customer drawing 776163. That proposal duplicated pad 9; the pad at (14 mm, 4 mm) is **pin 16** here.

Pad size 2.35 mm and drill 1.75 mm are taken from that proposal, not re-measured against drawing rev K1 (2024). **Do not fabricate from this footprint until the hole chart is checked against ENG_CD_776163.**

Cavity numbering follows that proposal (mating-face / TE convention):

- Row nearest the PCB edge in the footprint (y = 0): pins 1–12 at 4 mm pitch
- Middle row, offset 2 mm: pins 13–23
- Far row: pins 24–35

## Connector A — J30 (pins 1–35)

Outputs and high-current returns. Injectors, coils, and low-sides are grouped so a loom can break them out as bundles.

| Pin | Signal | Was |
| ---: | --- | --- |
| 1 | `+12V_RAW` | J3-1 |
| 2 | `+12V` | J4-8 |
| 3 | `12V_KEY` | J4-7 |
| 4 | `GND` | J4-3 |
| 5 | `GND` | J4-4 |
| 6 | `GND` | extra return, same `GND` net (third pin; rev E harness had two on J4) |
| 7 | `OUT_INJ1` | J5-6 |
| 8 | `OUT_INJ2` | J5-5 |
| 9 | `OUT_INJ3` | J5-4 |
| 10 | `OUT_INJ4` | J5-3 |
| 11 | `OUT_INJ5` | J5-2 |
| 12 | `OUT_INJ6` | J5-1 |
| 13 | `OUT_IGN1` | J5-15 |
| 14 | `OUT_IGN2` | J5-14 |
| 15 | `OUT_IGN3` | J5-12 |
| 16 | `OUT_IGN4` | J5-11 |
| 17 | `OUT_IGN5` | J5-13 |
| 18 | `OUT_IGN6` | J5-10 |
| 19 | `OUT_LS1` | J5-7 |
| 20 | `OUT_LS2` | J5-18 |
| 21 | `OUT_LS3` | J5-17 |
| 22 | `OUT_LS4` | J5-16 |
| 23 | `OUT_LS_HOT1` | J5-9 |
| 24 | `OUT_LS_HOT2` | J5-8 |
| 25 | `OUT_DC1+` | J4-5 |
| 26 | `OUT_DC1-` | J4-1 |
| 27 | `OUT_DC2+` | J4-6 |
| 28 | `OUT_DC2-` | J4-2 |
| 29 | `WBO_Heater` | J3-3 |
| 30 | `WBO_Ip` | J3-5 |
| 31 | `WBO_Un` | J3-4 |
| 32 | `WBO_Vm` | J3-6 |
| 33 | `WBO_Rtrim` | J3-2 |
| 34 | spare | no net |
| 35 | spare | no net |

## Connector B — J31 (pins 1–35)

Sensor reference, CAN, and inputs.

| Pin | Signal | Was |
| ---: | --- | --- |
| 1 | `+5VP` | J2 / J10 (one of four paralleled pins) |
| 2 | `+5VP` | paralleled |
| 3 | `+5VP` | paralleled |
| 4 | `GNDA` | J2 / J10 (one of five paralleled pins) |
| 5 | `GNDA` | paralleled |
| 6 | `GNDA` | paralleled |
| 7 | `GNDA` | paralleled |
| 8 | `GND` | J2-8 |
| 9 | `CAN+` | J10-7 |
| 10 | `CAN-` | J10-8 |
| 11 | `IN_MAP` | J10-9 |
| 12 | `IN_TPS1` | J10-13 |
| 13 | `IN_TPS2` | J2-14 |
| 14 | `IN_PPS1` | J10-6 |
| 15 | `IN_PPS2` | J2-4 |
| 16 | `IN_IAT` | J10-15 |
| 17 | `IN_CLT` | J10-16 |
| 18 | `IN_FLEX` | J10-5 |
| 19 | `IN_KNOCK_RAW` | J10-14 |
| 20 | `IN_AUX1` | J10-1 |
| 21 | `IN_AUX2` | J2-3 |
| 22 | `IN_AUX3` | J2-15 |
| 23 | `IN_BUTTON1` | J10-2 |
| 24 | `IN_BUTTON2` | J10-10 |
| 25 | `IN_BUTTON3` | J2-9 |
| 26 | `IN_HALL1` | J2-5 |
| 27 | `IN_HALL2` | J2-6 |
| 28 | `IN_HALL3` | J2-7 |
| 29 | `VR_MAX9924+` | J2-16 |
| 30 | `VR_MAX9924-` | J2-17 |
| 31 | `VR_DISCRETE+` | J2-18 |
| 32 | `VR_DISCRETE-` | J2-19 |
| 33 | `EGT+` | J2-10 |
| 34 | `EGT-` | J2-20 |
| 35 | spare | no net |

## Signals that do not get their own harness pin

Every **unique** rev E harness net is present. What does not fit as a separate pin:

- One of the four paralleled `+5VP` pins (J2 had two, J10 had two). The net is still on J31 pins 1–3.
- One of the five paralleled `GNDA` pins (J2 had three, J10 had two). The net is still on J31 pins 4–7.
- J30 pins 34–35 and J31 pin 35 are spare.

Not moved onto the 70-pin loom (they were not Mini-Fit harness connectors):

- USB: J8 mini-USB, J9 USB-C, and J7 Molex SPOX 5267-05A (`VBUS`, `USB+`, `USB-`, `GND`).
- 2.54 mm module jumpers (J1, J6, J11–J22, J24, and the second schematic `J5` where present). These are Hellen-One breakouts between modules, not the vehicle loom.

## Hellen-One / mechanical constraints

- Hellen-One modules (MCU, power, ign, inputs, WBO, VR, CAN, knock) are closed symbols. This change does not open them. Nets stop at the existing module pins.
- Mechanical placement is in [ampseal-35-mechanical.md](ampseal-35-mechanical.md). The outline is a 100 × 136 mm rounded rectangle (same width as rev E). J30 is on the bottom edge and J31 is on the top edge. Pin assignment is unchanged.
- Segments that ended on the old Mini-Fit pads were removed. Nets are not routed to the new headers; see [ampseal-35-unrouted.md](ampseal-35-unrouted.md).
- Firmware pin names are unchanged.
