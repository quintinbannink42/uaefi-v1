# Ordering the SUPERSEAL 60 harness

Smart-coil ignition only. One TE 6437288-5 on the right edge. Pinout: [superseal-60-pinout.md](superseal-60-pinout.md). Placement: [superseal-60-mechanical.md](superseal-60-mechanical.md).

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

Stackup is 4-layer, 1 oz (0.035 mm). IPC-2221, 10 °C rise, external `k = 0.048`, internal `k = 0.024`:

| Width | External | Internal |
|---|---|---|
| 0.25 mm | 0.9 A | 0.4 A |
| 0.40 mm | 1.2 A | 0.6 A |
| 0.55 mm | 1.6 A | 0.8 A |

The 3 mm pad pitch leaves a 0.7 mm gap. With 0.15 mm clearance the widest track that can leave a pad in a straight line is **0.40 mm**. Middle-row pads are staggered 1.5 mm, so those necks are **0.25 mm**. A 0.55 mm via pad / 0.30 mm drill (the board minimum hole is 0.30 mm) is about 1 A, and it is the practical continuous limit once the track is wider than the via.

Drawn harness copper:

| Class | Nets | Drawn width |
|---|---|---|
| High current | `+12V`, `+12V_RAW`, `12V_KEY`, `GND`, `WBO_Heater`, `OUT_INJ*`, `OUT_LS*`, `OUT_LS_HOT*`, `OUT_DC*` | 0.40 mm on the side lane and on the F.Cu row when that row is clear. The neck through the pin field is still 0.25 mm. |
| Sensors, CAN, VR, EGT, coil logic | everything else on J30 | 0.25 mm |

Do not rate a pin at the Superseal “15 A” catalog figure, and do not rate `+12V` or a DC output at 5–8 A. VNLD5160 and TLE9201 can be asked for more current than this 1 oz neck can bring to the pin. Fuse each high-current channel at **1 A continuous** unless the neck is widened on a heavier copper revision. Two GND pins share the return; they do not make a 15 A ground.

`+5VP` and `GNDA` are one pin each. Coil outputs are logic, not coil current.

## DRC (KiCad 8, errors)

No shorts and no crossing tracks. New vias are 0.55 mm pad / 0.30 mm drill, which clears the minimum hole.

Still open, and not a clean fab sign-off:

- 21 J30 pads listed in the pinout doc are still unconnected.
- Clearance violations remain on harness tracks that pass existing vias and on copper that was already tight. The previous AMPSEAL board also reported a large clearance set.
- A few new tracks enter the Bluetooth keepout and run close to the outline.
- Solder-mask bridges remain near the left mounting holes where a route passed H1/H2. Vias that drilled into H1, H2, or a U3 pad were removed.

## Removed from the carrier

2.54 mm 2×02 sockets, not the Hellen-One mezzanine: **J1, J11, J12, J13, J14, J15, J16, J17, J18, J19, J20, J21, J22, J24**.

Kept: modules M1–M7, J6 (1×06), J7 (Molex SPOX), USB J8/J9, mounting holes H1–H4.
