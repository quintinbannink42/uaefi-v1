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

Widths below are the thinnest track longer than about 3 mm on the left-edge route. Net classes in the project file are unchanged (`PWR` 2.4, `HC` 1.2, `LS` 1.0, `IGN` 0.40). The pin field and the escape channel necked most power nets below those classes. No pin was re-paralleled.

| Net | Series copper (thinnest run > ~3 mm) | Continuous, 1 oz, 10 °C, external | Fuse note |
|---|---|---|---|
| `+12V` | 0.55 mm | ~1.6 A | Class is 2.4 mm. The left-edge escape does not hold that width. Fuse near 1.5 A until the neck is widened. |
| `+12V_RAW` | 0.50 mm | ~1.5 A | Fuse near 1.5 A. |
| `12V_KEY` | 0.24 mm | ~0.9 A | Fuse near 1 A. |
| `GND` | plane, plus the two header pins | plane | Two pins share the return. |
| `OUT_INJ2`, `OUT_DC1+`, `OUT_DC1−`, `OUT_DC2+`, `OUT_DC2−`, `OUT_LS1`, `OUT_LS_HOT1` | 0.55 mm | ~1.6 A | Injector and motor current is pulsed or intermittent. Fuse each near 1.5 A continuous. |
| `OUT_INJ3`, `OUT_LS2`, `OUT_LS3`, `OUT_LS4` | 0.50 mm | ~1.5 A | Same note. |
| `OUT_INJ1`, `OUT_INJ4`, `OUT_INJ5`, `OUT_INJ6`, `WBO_Heater`, `OUT_LS_HOT2` | 0.24 mm | ~0.9 A | Heater duty is closer to continuous. Fuse the heater near 1 A. |
| `OUT_IGN6` | 0.40 mm | logic | Smart-coil gate drive. |
| `OUT_IGN1`, `OUT_IGN2` | 0.24 mm | logic | Gate drive. |
| `OUT_IGN3`, `OUT_IGN4`, `OUT_IGN5` | 0.15 mm | logic | Gate drive. The 0.40 mm class does not fit these escapes. |
| `+5VP` | 0.40 mm | signal / low current | |
| Sensors, CAN, `GNDA`, VR | 0.20–0.25 mm | signal | `CAN±` and `GNDA` neck to 0.20 mm. |

## DRC (KiCad 8.0.9, errors only)

Every used J30 pad, including both GND pins, has same-net copper on the pad. No harness pins were re-paralleled. New vias are 0.55 mm pad / 0.30 mm drill.

Compared with the right-edge board (0 shorts, 0 crossing tracks, 9 unconnected, 500 clearance, 196 hole-clearance, 188 items-not-allowed):

- Shorts: **46**. These are harness tracks crossing module GND fingers and a few driver pads. There are **0 crossing tracks**.
- Unconnected items: 19. They are islands and layer changes, not open J30 pads.
- Clearance: 77. `items_not_allowed`: 37. Solder-mask bridge: 26. Hole-to-hole: 12.
- No copper-to-edge errors on this outline.
- Cavity 1 of 6437288-5 is still unverified: TE returned HTTP 403 for `JPN_CD_6437288-5`.

## Removed from the carrier

2.54 mm 2×02 sockets, not the Hellen-One mezzanine: **J1, J11, J12, J13, J14, J15, J16, J17, J18, J19, J20, J21, J22, J24**.

Kept: modules M1–M7, J6 (1×06), J7 (Molex SPOX), USB J8/J9, mounting holes H1–H4.
