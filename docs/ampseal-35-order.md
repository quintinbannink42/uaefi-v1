# Ordering this uaEFI AMPSEAL fork

Smart-coil ignition only. Two AMPSEAL 35 headers on a 100 × 136 mm rounded rectangle.

## Board

| Item | Value |
| --- | --- |
| Outline | x 50–150 mm, y 42–178 mm (100 × 136 mm), 3.5 mm corner radius |
| Stackup | 4 copper layers, 1.6 mm (see the board setup in `uaefi.kicad_pcb`) |
| Headers | Two TE **776163-1** (35 pos, right angle, key 1, tin). Gold option is 1-776163-1. |
| Plugs | Two TE **776164-1** housings, terminals 770520 (reel) or 770854 (loose) |
| Mounting | Existing M3 holes H1–H4, inset from the new top and bottom edges |
| Ignition | Logic-level smart coils on J30 `OUT_IGN1`–`OUT_IGN6`. Onboard IGBTs Q7–Q12 (ISL9V3040D3ST) are removed from the board and the BOM. |

Pinout: [ampseal-35-pinout.md](ampseal-35-pinout.md). Placement: [ampseal-35-mechanical.md](ampseal-35-mechanical.md). Carrier BOM dumped from the PCB: [ampseal-35-bom.csv](ampseal-35-bom.csv).

## Footprint check

`footprints/TE_AMPSEAL_35_776163-1.kicad_mod` was compared with the text of TE customer drawing 776163 rev K1:

- 35 circuits, 3 rows, right-angle, 4 mm pitch: matches the drawing.
- Drill 1.75 mm: matches the drawing note “35X 1.75”.
- Body length in the footprint is 76.8 mm; the drawing lists 76.9 mm.
- The drawing’s recommended hole chart on sheet 2 is a graphic. The X/Y of each pin, including the 2 mm middle-row offset, comes from KiCad footprint proposal #633 with pad 16 corrected (that file had a duplicate pad 9). Pad diameter 2.35 mm is from that proposal, not from a re-measured annular ring.

Before a production panel, open ENG_CD_776163 in KiCad 8 and confirm the hole chart. Do not treat this footprint as fully digitized from the drawing.

## Fab outputs

This tree’s board file is KiCad 8 (`generator_version` 8.0). The build environment here has KiCad 7.0.11, which refuses the file, so Gerbers, drill, and IPC-D-356 were **not** regenerated. In KiCad 8:

1. Refill zones (the GND pour outline now matches the 100 × 136 mm board; the fill polygons are still the old 100 × 100 mm pour).
2. Run DRC. Expect to clean the six direct routes listed in [ampseal-35-unrouted.md](ampseal-35-unrouted.md).
3. Plot Gerbers and drill the same way as the existing `gerber/` outputs (F.Cu, In1.Cu, In2.Cu, B.Cu, masks, silk, edge cuts).
4. Export a position file. Q7–Q12 must not appear.

## Loom

J30 is the bottom header (power, injectors, smart-coil ignition, low-side, DC, wideband). J31 is the top header (5 V, sensor ground, CAN, inputs, VR, EGT). Same pin assignment as the pinout doc.
