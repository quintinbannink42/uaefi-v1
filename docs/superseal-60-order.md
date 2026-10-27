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

Widths below are the thinnest track longer than about 3 mm after the header moved onto the core. Net classes in the project file are unchanged (`PWR` 2.4, `HC` 1.2, `LS` 1.0, `IGN` 0.40). The 3 mm pin field still cannot hold those classes: a 2.3 mm pad on a 3 mm pitch leaves a 0.7 mm gap, and 0.15 mm clearance makes 0.40 mm the widest track that fits. Outside the field the escape widens where it can. No pin was re-paralleled.

| Net | Series copper (thinnest run > ~3 mm) | Continuous, 1 oz, 10 °C, external | Fuse note |
|---|---|---|---|
| `+12V`, `+12V_RAW`, `GND` | 0.40 mm | ~1.2 A | Class is 2.4 mm. The pin-field gap is the limit. Fuse near 1 A until that neck is a plane or a parallel pin. |
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

Every used J30 pad was connected on the previous left-edge board, including both GND pins. Cavity numbers are unchanged. New vias are 0.55 mm pad / 0.30 mm drill. The old socket pin-name legend (186 silkscreen labels) is removed. The only added connector mark is the footprint’s silkscreen “1” at (29.4, 140.6).

Compared with that board (squash `57590d2`, the PR #3 layout):

| Check | PR #3 (151.2 × 112.1) | This layout (125 × 100) |
|---|---|---|
| Shorts | 46 | **0** |
| Crossing tracks | 0 | **0** |
| Unconnected items | 19 | 81 |
| Open J30 pads | 0 | **6** |
| Clearance | 79 | **33** |
| Copper-to-edge | 0 | **0** |
| Solder-mask bridge | 26 | 2 |
| Items not allowed | 37 | 36 |
| Hole-to-hole | 12 | 12 |

A re-run on KiCad 8.0.9 after the `OUT_IGN3` / `OUT_IGN5` width change matches this table: 0 shorts, 0 crossing tracks, 81 unconnected items, 6 open J30 pads, 33 clearance.

The 46 shorts were harness tracks through module GND fingers and driver pads. Those tracks were deleted and the escape was drawn again around the fingers.

Six header pads are still open. A bounded search, one net at a time, did not find a path that keeps shorts at 0, crossing tracks at 0, and the board's own hole and clearance rules.

Pins 47, 46, 45, 38, and 37 (`IN_HALL3`, `IN_HALL2`, `IN_HALL1`, `VR_MAX9924+`, `EGT−`) all have to cross x ≈ 32.2, the 0.7 mm slot between the outer and inner pad columns. `IN_BUTTON3` already fills that slot on In1.Cu and `IN_BUTTON2` fills it on In2.Cu, from about y = 81 to y = 92. The front-to-outer column gap is 0.2 mm, so a track cannot step sideways around those two verticals. F.Cu and B.Cu are open on the stagger rows y = 84.5 and y = 87.5 only. East of the inner pads the same rows sit inside the 0.40 mm outer keepout of `OUT_IGN4` / `OUT_IGN5` / `OUT_IGN6`, so the track has to change layer in the pocket at about (32.7, 84.5) or (32.7, 87.5). That pocket fits a 0.40 mm via with a 0.20 mm drill. It does not fit a via that meets this board's limits (0.30 mm minimum hole, 0.10 mm minimum annular ring, so 0.50 / 0.30 mm). Each of those two rows can carry one track, and neither row has a legal via, so none of the five pins can leave the header.

Pin 11 `WBO_Un` is closed on the south by the F.Cu `GNDA` bar at y = 139.5 and by the `+12V` / `+12V_RAW` copper on the inner layers. Moving that bar south does open a path. It also lets the F.Cu GND pour reach outer ignition tracks at the pour's 0.20 mm clearance, about 110 new ignition clearance errors. The bar stays where it is.

Post-field `+12V`, `+12V_RAW`, and `GND` were measured for a wider track and for a parallel track on the other layers. The copper beside those runs (vias and pads already at the clearance limit, no free 0.6 mm channel on F.Cu, In2.Cu, or B.Cu) does not allow a wider section. The 0.40 mm neck remains.

| Pin | Net | Core copper still on the board |
|---|---|---|
| 47 | `IN_HALL3` | In1.Cu, about 5.3 mm, not reaching the header |
| 46 | `IN_HALL2` | B.Cu, about 6.7 mm |
| 45 | `IN_HALL1` | B.Cu, about 14.7 mm |
| 38 | `VR_MAX9924+` | In1.Cu, about 72.5 mm |
| 37 | `EGT−` | In1.Cu, about 12.0 mm |
| 11 | `WBO_Un` | F.Cu, about 7.0 mm |

Cavity 1 of 6437288-5 is still unverified: TE returned HTTP 403 for `JPN_CD_6437288-5`.

## Removed from the carrier

2.54 mm 2×02 sockets, not the Hellen-One mezzanine: **J1, J11, J12, J13, J14, J15, J16, J17, J18, J19, J20, J21, J22, J24**.

Kept: modules M1–M7, J6 (1×06), J7 (Molex SPOX), USB J8/J9, mounting holes H1–H4.
