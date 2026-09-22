# AMPSEAL 35 mechanical placement

Placement pass on top of the dual-header net assignment. Pinout is unchanged (`docs/ampseal-35-pinout.md`). No pin swaps.

## Footprint size (hypothesis)

`footprints/TE_AMPSEAL_35_776163-1.kicad_mod` still follows the abandoned KiCad proposal for TE drawing 776163, not a re-measure of rev K1.

| Feature | Local coordinates (pin 1 at 0,0) |
| --- | --- |
| Fab body | x −16.4 to 60.4 mm, y −2.9 to 35.85 mm (76.8 × 38.75 mm) |
| Courtyard | x −17.2 to 61.2 mm, y −3.7 to 36.6 mm |
| Pin rows | y = 0 (pins 1–12), y = 4 (pins 13–23, x offset 2 mm), y = 8 (pins 24–35); pitch 4 mm |
| Alignment holes | (−6.5, 4.5) and (50.5, 4.5), drill 2.85 mm |
| Pad drill | 1.75 mm, pad 2.35 mm (unverified) |

TE drawing 776163 also lists an overall length of 76.9 mm, a width of 37.9 mm, and a profile height off the PCB of 23.6 mm. The footprint’s long axis matches that length. The 38.8 mm local depth is the right-angle body lying in the board plane (mating direction), not the vertical height.

**Keep-out used for this pass:** every plated pad, including the two alignment holes, stays at least 1.5 mm inside the outline. The mating body past local y ≈ 12 mm hangs off the edge, which is how these right-angle headers are usually mounted. Do not treat the courtyard rectangle as copper keep-out; most of it is the overhanging shell.

## Outline

Rev E was a 100 × 100 mm rounded rectangle, x 50–150 mm, y 60–160 mm, 3.5 mm corner radii, M3 holes H1–H4 at the four corners.

Two 77 mm headers do not fit on that outline. The board grows only as two rectangular tabs. Corner holes, radii, USB, and Hellen-One modules stay put.

| Region | Outline | Added area |
| --- | --- | --- |
| Main board | x 50–150, y 60–160 | unchanged |
| Bottom tab (J30) | x 58–124, y 160–178 | 66 × 18 mm |
| Right tab (J31) | x 150–180, y 70–150 | 30 × 80 mm |

Axis-aligned bounding box of the new outline: **130 × 118 mm** (x 50–180, y 60–178).

## Connector positions

KiCad rotation is the file convention verified against the old Mini-Fit pads (positive angle, Y downward in the file).

| Ref | Position | Rotation | On-board pin field | Body |
| --- | --- | --- | --- | --- |
| J30 | (68.4, 166) | 0 | x ≈ 61–120, y ≈ 165–175 | hangs below y = 178, toward +Y |
| J31 | (168, 132) | 90 | x ≈ 167–177, y ≈ 80–140 | hangs past x = 180, toward +X |

Clearance checked against pad and graphic bounds of the other footprints:

- J30’s shell starts at y ≈ 163. USB-C J9 ends at y ≈ 160.2. J7 (SPOX) is at x ≈ 131–137, outside the tab (tab ends at x = 124).
- J31’s shell starts at x ≈ 165. The WBO module M5 reaches x ≈ 163.4 and J6 reaches x ≈ 163. Gap is about 1.7 mm. That gap is only as good as the footprint outline; re-check when the TE drawing is confirmed.
- Mounting holes H1–H4 are outside both tabs.

Nothing else was moved.

## Copper

72 track segments that ended on the removed Mini-Fit pads (J2, J3, J4, J5, J10) were deleted. Vias were not on those pads. Routes that still touch a module or discrete pad were left, so many nets now end in a stub. There is no new routing from the modules to J30 or J31.

Which header pads have no track on them: [docs/ampseal-35-unrouted.md](ampseal-35-unrouted.md).

## Fabrication caveats

- Confirm drills, pad sizes, pin numbering, and the overhang against ENG_CD_776163 before ordering boards.
- The tabs are square. The original corner radii are unchanged.
- J30 and J31 use the same key-1 footprint. A second key (776163-2 / -4 / -5) would need a different shell, not a different pad map.
- Orphaned Mini-Fit stubs that still connect to a real pad were not ripped back to the modules.
