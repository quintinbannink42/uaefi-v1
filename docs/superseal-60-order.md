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

| Net | Series copper | Continuous, 1 oz, 10 °C, external | Fuse note |
|---|---|---|---|
| `+12V` | 2.4 mm (3.0 mm on the south corridor) | ~4.5 A | Fuse the feed near 5 A. The corridor is locally 3.0 mm on F and B; the series section is the 2.4 mm run, not 5–8 A. |
| `+12V_RAW` | 1.5 mm (3.0 mm corridor does not continue) | ~3.2 A | Fuse near 3 A. |
| `12V_KEY` | 0.80 mm over tens of millimetres | ~2.0 A | The 3.0 mm corridor stops. Fuse near 2 A. |
| `GND` | plane on all four layers, plus wide spokes at the two header pins | plane | Two pins share the return. Do not add the Superseal rating twice. |
| `OUT_INJ1`, `OUT_INJ3`, `OUT_INJ5`, `OUT_INJ6` | 1.2 mm | ~2.7 A | Injector current is pulsed. Fuse each channel near 2 A continuous. Peaks can sit above the IPC steady-state number for the pulse width; they cannot sit at 15 A. |
| `OUT_INJ2` | 0.80 mm | ~2.0 A | Same pulse note. Fuse near 2 A. |
| `OUT_INJ4` | 0.35 mm for about 140 mm | ~1.1 A | The 1.2 mm class did not fit this channel. Fuse near 1 A. |
| `OUT_DC2+` | 1.0 mm | ~2.4 A | Motor current is longer than an injector pulse. Fuse near 2 A. |
| `OUT_DC1+` | 0.80 mm | ~2.0 A | Fuse near 2 A. |
| `OUT_DC1−`, `OUT_DC2−` | 0.55 mm | ~1.6 A | Fuse near 1.5 A. |
| `WBO_Heater` | 1.2 mm, with a few millimetres at 1.0 mm | ~2.5 A | Heater duty is closer to continuous than an injector. Fuse near 2.5 A. |
| `OUT_LS2`, `OUT_LS3`, `OUT_LS_HOT1`, `OUT_LS_HOT2` | 1.0–1.2 mm | ~2.4–2.7 A | Fuse near 2 A. |
| `OUT_LS4` | 0.30 mm for about 66 mm after the 1.0 mm run | ~1.0 A | Fuse near 1 A. |
| `OUT_LS1` | 1.0 mm for most of the run, then about 20 mm at 0.25 mm | ~0.9 A | The thin section sets the rating. Fuse near 1 A. |
| `OUT_IGN1`–`OUT_IGN6` | 0.40 mm | logic | Smart-coil gate drive, not coil current. |
| Sensors, CAN, VR, EGT, `+5VP`, `GNDA` | 0.25–0.40 mm | signal | `VR_MAX9924−` uses a 0.15 mm fanout where the pin field would not pass 0.25 mm. |

## DRC (KiCad 8.0.9)

No shorts and no crossing tracks. New vias are 0.55 mm pad / 0.30 mm drill. Every J30 signal pad reaches another pad on its net. Both GND header pins tie into the plane.

Still not a clean fab sign-off:

- Clearance violations remain (about 360), including harness tracks beside existing vias and copper that was already tight.
- `items_not_allowed` is unchanged at 188 (footprints and keepouts that predate this route, including the Bluetooth keepout).
- 22 connection-width reports, mostly GND, plus the `VR_MAX9924−` fanout and short necks on `OUT_LS2`, `OUT_LS4`, and `OUT_DC1−`.
- 9 unconnected items are dangling islands on nets whose header pin is already tied to a driver pad (M2 GND, a few millimetres of `OUT_DC2−`, `+5VP`, buttons, `OUT_IGN2`, `OUT_INJ6`, and the onboard `LS_HOT` stubs). They are not open header pads.
- 6 copper-to-edge and 24 solder-mask-bridge reports remain. Hole-to-hole spacing reports 12.
- Cavity 1 of 6437288-5 is still unverified: TE returned HTTP 403 for `JPN_CD_6437288-5`.

## Removed from the carrier

2.54 mm 2×02 sockets, not the Hellen-One mezzanine: **J1, J11, J12, J13, J14, J15, J16, J17, J18, J19, J20, J21, J22, J24**.

Kept: modules M1–M7, J6 (1×06), J7 (Molex SPOX), USB J8/J9, mounting holes H1–H4.
