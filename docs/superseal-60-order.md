# Ordering the SUPERSEAL 60 harness

Smart-coil ignition only. One TE 6437288-5 on the left edge. Pinout: [superseal-60-pinout.md](superseal-60-pinout.md). Placement: [superseal-60-mechanical.md](superseal-60-mechanical.md).

## Buy

| Item | Part |
|---|---|
| PCB header | TE **6437288-5** (SUPERSEAL 1.0, 60 pos, 4 row, right angle, gold) |
| 34-pos plug | **4-1437290-0** for pins 1–34 |
| 26-pos plug | **3-1437290-7** for pins 35–60 |
| Ignition | Logic-level smart coils on `OUT_IGN1`–`OUT_IGN6`. Onboard IGBTs Q7–Q12 stay off the board and out of the BOM. |

Confirm plug keying against the TE drawing before crimping a loom. The product PDF `JPN_CD_6437288-5` was not available here (TE returned HTTP 403).

Carrier BOM for the connector change: [superseal-60-bom.csv](superseal-60-bom.csv).

## Current the copper can actually carry

Stackup is 4-layer, **1 oz (0.035 mm) on every copper layer**. IPC-2221, 10 °C rise, external `k = 0.048`, internal `k = 0.024`:

| Width | External | Internal |
|---|---|---|
| 0.25 mm | 0.9 A | 0.4 A |
| 0.30 mm | 1.0 A | 0.5 A |
| 0.35 mm | 1.1 A | 0.6 A |
| 0.40 mm | 1.2 A | 0.6 A |
| 0.55 mm | 1.6 A | 0.8 A |
| 0.80 mm | 2.0 A | 1.0 A |
| 1.0 mm | 2.4 A | 1.2 A |
| 1.2 mm | 2.7 A | 1.4 A |
| 1.5 mm | 3.2 A | 1.6 A |
| 2.4 mm | 4.5 A | 2.3 A |
| 3.0 mm | 5.3 A | 2.7 A |

Net classes in `uaefi.kicad_pro` set the default width (clearance stays 0.15 mm, so existing tight copper is not a new class error). The class is the target. The continuous rating is the thinnest section longer than about 3 mm on the path from the header to the driver. A short pin-field neck does not set the fuse. A long thin run does, even if a wide spine sits in parallel. One 0.30 mm drill via is roughly 0.8 A; the wide nets use several vias at each layer change.

Do not rate a pin at the Superseal “15 A” catalog figure. That number is the contact, not this 1 oz board.

The new J30 fanout is 0.20 mm, including the run south of the pin field. That is now the series neck on every net that was redrawn from the header. Net classes are unchanged (`PWR` 2.4, `HC` 1.2, `LS` 1.0, `IGN` 0.40) and were not reached on this pass: the 2.3 mm pads on a 3 mm pitch leave a 0.7 mm gap, and the copper past the field is already inside the ignition keepout or against a neighbor. No 0.40 / 0.20 mm via was added. Vias on the new routes are 0.55 mm pad / 0.30 mm drill. The drill file has no 0.20 mm tool.

| Net | Series copper (thinnest run > ~3 mm) | Continuous, 1 oz, 10 °C, external | Fuse note |
|---|---|---|---|
| `+12V`, `+12V_RAW`, `GND`, and the redrawn J30 nets | 0.20 mm | ~0.8 A | New fanout from the north header. Class widths were not reached on this pass. |
| `12V_KEY` | 0.24 mm | ~0.9 A | Fuse near 1 A. |
| `OUT_DC1+`, `OUT_DC1−`, `OUT_INJ4`, `OUT_INJ5`, `OUT_LS3` | 0.50 mm | ~1.5 A | Pulsed. Fuse near 1.5 A continuous. |
| `OUT_INJ2`, `OUT_INJ3`, `OUT_LS1`, `OUT_LS2`, `OUT_LS4`, `OUT_LS_HOT1` | 0.40 mm | ~1.2 A | Same note. |
| `OUT_DC2+`, `OUT_DC2−` | 0.25 mm | ~0.9 A | Class is 1.2 mm. Fuse near 1 A. |
| `OUT_INJ1`, `OUT_INJ6`, `WBO_Heater`, `OUT_LS_HOT2` | 0.24 mm | ~0.9 A | Heater duty is closer to continuous. Fuse the heater near 1 A. |
| `OUT_IGN6` | 0.25 mm | logic | Smart-coil gate drive. Class is 0.40 mm. |
| `OUT_IGN1`, `OUT_IGN2` | 0.24 mm | logic | Gate drive. |
| `OUT_IGN3` | 0.40 mm | logic | The 3.2 mm In1.Cu run at y = 111.6 is now the class width. |
| `OUT_IGN4` | 0.15 mm | logic | B.Cu run of 12.5 mm. An `/INJ5` via at (61.9, 108.6) leaves no room to grow it under the 0.40 mm outer ignition clearance. |
| `OUT_IGN5` | 0.15 mm | logic | The F.Cu run from (58, 94) to (69.5, 94.5) is now 0.35 mm. The 26.2 mm F.Cu run and two ~4 mm runs stay 0.15 mm, against the `/IN_PPS2` via at (74.0, 113.2). |
| `+5VP` | 0.25 mm | signal / low current | |
| `GNDA` | 0.20 mm | signal | |
| Sensors, CAN, VR, EGT | 0.15–0.20 mm | signal | Several new escapes are 0.15 mm for more than 3 mm. |

## DRC (KiCad 8.0.9)

North-edge placement, proto grids removed, header rerouted with the existing via rule (0.55 / 0.30 mm). No new rule area and no 0.20 mm drill.

| Check | PR #3 (151.2 × 112.1) | This layout (101.0 × 115.2) |
|---|---|---|
| Shorts | 46 | **0** |
| Crossing tracks | 0 | **0** |
| Unconnected items | 19 | 87 |
| Open J30 pads | 0 | **1** (`+5VP`, pin 7) |
| Clearance | 79 | 171 |
| Solder-mask bridge | 26 | 2 |
| Items not allowed | 37 | 36 |
| Hole-to-hole | 12 | 12 |

159 of the clearance hits are the outer ignition rule (0.40 mm). The new `OUT_IGN*` fanout runs on outer copper inside that keepout. The two solder-mask bridges are the existing `/12V_KEY` via.

Pin 7 `+5VP` is the open pad. It sits on the south row between `GNDA`, `/WBO_Heater`, and `+12V_RAW`. Those neighbors already occupy the stagger gaps, and a 0.55 / 0.30 mm via does not fit between the 2.3 mm pads. A 0.40 / 0.20 mm via was not added in this pass.

`OUT_IGN1`, `OUT_IGN2`, and `OUT_IGN3` leave the header but their core crossing is only the escape; KiCad still counts the pads as connected through copper the escape touches. `VR_MAX9924+` and `+12V_RAW` are the same kind of partial route and are connected in DRC.

## Proto parts removed that had a net

| Ref | Net | Still on the board |
|---|---|---|
| P1 | `Net-(M7-CANL)` | M7 |
| P2 | `Net-(M7-CANH)` | M7 |
| P5 | `/VR_DISCRETE` | M3, M6 |
| P6 | `/VR_MAX9924` | M4, M6 |
| G3 | `+12V_RAW`, `+3.3VA`, `+5VA`, `GND` | yes, elsewhere |
| G4 | `Net-(G4-Pad1)`, `Pad10`, `Pad12`, `Pad13`, `Pad14` | no. These nets existed only on the proto grid |

Cavity 1 of 6437288-5 is still unverified: TE returned HTTP 403 for `JPN_CD_6437288-5`.

## Removed from the carrier

2.54 mm 2×02 sockets, not the Hellen-One mezzanine: **J1, J11, J12, J13, J14, J15, J16, J17, J18, J19, J20, J21, J22, J24**.

Kept: modules M1–M7, J6 (1×06), J7 (Molex SPOX), USB J8/J9, mounting holes H1–H4.
