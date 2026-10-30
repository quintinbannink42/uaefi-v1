# Ordering the SUPERSEAL 60 harness

Smart-coil ignition only. One TE 6437288-5 on the north edge. Pinout: [superseal-60-pinout.md](superseal-60-pinout.md). Placement: [superseal-60-mechanical.md](superseal-60-mechanical.md).

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

## Track widths after the widening pass

Every segment of the J30 power, HC, LS and IGN nets was widened toward its class width in 0.05 mm steps, as wide as it can go while keeping 0.15 mm (0.40 mm for IGN on outer copper) to every other net, pad, hole and the board edge. Nothing was rerouted for width, so a segment boxed in by a neighbour keeps its old width. Inside the pin field the neck is set by the 0.7 mm gap between 2.3 mm pads (0.20–0.40 mm). **Class widths are mostly not reached outside the field either.** The board needs a real re-route of the power and output channels before it can carry rated current.

| Net | Class | Length at class width | Thinnest run | Continuous, 1 oz, 10 °C, external |
|---|---|---|---|---|
| `+12V` | 2.4 | 2.4 of 213 mm | 0.20 mm | ~0.8 A |
| `+12V_RAW` | 2.4 | 8.4 of 463 mm | 0.20 mm (main run 0.40 mm) | ~0.8 A |
| `12V_KEY` | 2.4 | 4.6 of 317 mm | 0.20 mm | ~0.8 A |
| `OUT_INJ1`–`OUT_INJ6` | 1.2 | 3–11 % of each net | 0.20 mm | ~0.8 A |
| `OUT_DC1±`, `OUT_DC2±` | 1.2 | 3–26 % | 0.20 mm | ~0.8 A |
| `OUT_LS_HOT1/2`, `WBO_Heater` | 1.2 | 3–16 % | 0.20 mm | ~0.8 A |
| `OUT_LS1`–`OUT_LS4` | 1.0 | 2–24 % | 0.20 mm | ~0.8 A |
| `OUT_IGN1`–`OUT_IGN6` | 0.40 | 27–73 % | 0.20 mm (IGN4, IGN5: 0.15 mm) | logic |
| `+5VP` | — | — | 0.20 mm neck, 0.30–0.40 mm route | signal |

Fuse every output as if it were a 0.20 mm track until these are re-routed.

## Vias

Every via is 0.55 / 0.30 mm or larger (499 × 0.55/0.30, 8 × 0.60/0.30, 199 × 0.80/0.40). Pin 7 `+5VP` was routed with standard vias, so **no 0.20 mm drill was added**; the drill file has no 0.20 mm tool and no rule area or custom rule was needed.

## DRC (KiCad 8.0.9, zones refilled)

| Check | Before this pass (c4a9f0b) | Now |
|---|---|---|
| Shorts | 0 | **0** |
| Unconnected items | 87 | 27 |
| Open J30 nets | see below | 3 (`OUT_IGN2`, `OUT_IGN3`, `VR_MAX9924+`) |
| Clearance | 171 (stale zone fill) | 11 (6 of them the 0.40 mm IGN outer rule) |
| Solder-mask bridge | 2 | 0 |
| Items not allowed | 36 | 0 |
| Hole-to-hole | 12 | 12 (vias on top of same-net module pads) |

The previous "only pin 7 is open" count was wrong: the cloud-agent fanout left 16 nets split into separate copper islands. This pass removed 206 dead track/via islands and reconnected `+5VP` (J30.7 → R1 → M1.V4), `OUT_IGN1`, `OUT_LS1`–`OUT_LS4`, `+12V_RAW` (J30.2, D2–D5 → M1), `VR_MAX9924`, `LS_HOT1/2`, `+3.3VA` and `+5VA`.

Still open: `OUT_IGN2` (J30.49 → R21), `OUT_IGN3` (J30.50 → R22) and `VR_MAX9924+` (J30.38 → M4). The pad escapes exist but no clear path to the far end fits at 0.20 mm with 0.55 mm vias. 24 small `GND` islands (isolated SMD ground pads such as U7.5, U8.5/7, U10.5/7, C28, C30) do not reach the pour; these were already broken before this pass.

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
