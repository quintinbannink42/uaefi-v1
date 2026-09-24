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

Generated with KiCad 8.0.9 (`kicad-cli`). Files are in `fab/`:

| File | Use |
| --- | --- |
| `uaefi-F_Cu.gbr`, `uaefi-In1_Cu.gbr`, `uaefi-In2_Cu.gbr`, `uaefi-B_Cu.gbr` | Copper |
| `uaefi-F_Mask.gbr`, `uaefi-B_Mask.gbr` | Solder mask |
| `uaefi-F_Paste.gbr`, `uaefi-B_Paste.gbr` | Paste |
| `uaefi-F_Silkscreen.gbr`, `uaefi-B_Silkscreen.gbr` | Silkscreen |
| `uaefi-Edge_Cuts.gbr` | Board outline |
| `uaefi-PTH.drl`, `uaefi-NPTH.drl` | Excellon drill, plated and non-plated |
| `uaefi-pos.csv` | Pick-and-place (mm, CSV). Q7–Q12 are not on the board. |
| `uaefi-job.gbrjob` | Gerber job file |

JLCPCB / PCBWay upload: zip `fab/` and load the Gerbers plus both drill files. Set 4 layers, 1.6 mm, the stackup order F / In1 / In2 / B. Confirm the outline is 100 × 136 mm before paying.

The GND zone was refilled in KiCad 8. Its filled bounding box is the full outline (100 × 136 mm, y 42–178).

## DRC (KiCad 8.0.9, errors only)

| Check | Count |
| --- | --- |
| Shorts | 0 |
| Tracks crossing | 0 |
| Clearance | 103 |
| Copper edge clearance | 37 |
| Hole clearance | 20 |
| Solder-mask bridge | 19 |
| Items in keepout | 8 |
| Unconnected items | 101 |

The straight jumps that shorted `OUT_INJ6`, `OUT_DC1+`, `OUT_DC1-`, `OUT_DC2+`, `EGT+`, and `EGT-` were removed. A clearance-safe path through the Hellen-One modules does not exist for those nets, or for the other header pins listed in [ampseal-35-unrouted.md](ampseal-35-unrouted.md). They are open, not shorted. The remaining clearance, edge, hole, and mask errors are the same class as the stock race-core board (zone and silk/hole geometry). They are not a new short between AMPSEAL nets.

AMPSEAL hole-chart graphic on TE drawing 776163 sheet 2 is still not re-measured. Confirm it before a production panel.

## Loom

J30 is the bottom header (power, injectors, smart-coil ignition, low-side, DC, wideband). J31 is the top header (5 V, sensor ground, CAN, inputs, VR, EGT). Same pin assignment as the pinout doc.
