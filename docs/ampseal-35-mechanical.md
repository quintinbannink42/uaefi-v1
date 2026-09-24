# AMPSEAL 35 mechanical placement

Same family as the rusEFI uaEFI race core, not a clone. Modules, USB, and the four M3 holes stay where rev E put them. Only the outline and J31 moved so the two headers sit on opposite edges.

Pinout is unchanged (`docs/ampseal-35-pinout.md`).

## Outline

Clean rectangle with the same 3.5 mm corner radius as rev E. No side tabs.

| | Rev E race core | This fork |
| --- | --- | --- |
| X | 50–150 mm (100 mm) | 50–150 mm (100 mm) |
| Y | 60–160 mm (100 mm) | 42–178 mm (136 mm) |
| Corners | 3.5 mm radius | 3.5 mm radius |
| Mounting | H1–H4 at the four corners | H1–H4 unmoved, so they sit inset from the new top and bottom edges |

The extra 18 mm on the top and 18 mm on the bottom are the AMPSEAL pin seats. Mating shells hang off those edges.

## Connectors

KiCad file rotation (Y downward in the file), checked against the old Mini-Fit pads.

| Ref | Position | Rotation | Pin field (approx.) | Shell |
| --- | --- | --- | --- | --- |
| J30 | (68.4, 166) | 0 | x 61–120, y 165–175 | hangs below y = 178 |
| J31 | (112.4, 55) | 180 | x 61–120, y 46–56 | hangs above y = 42 |

Both headers use the same X span. J31 is rotated 180° so its shell leaves the top edge.

Clearance, using pad and graphic bounds:

- J31’s shell back is near y = 58. Mounting holes H1 and H4 start at y ≈ 61. The top row of 2.54 mm jumpers starts near y = 69.
- J30’s shell back is near y = 163. USB-C J9 ends near y = 160. J7 (SPOX) is to the right of the header body (body ends near x = 129, J7 starts near x = 131).

Nothing else was moved.

## Footprint

`footprints/TE_AMPSEAL_35_776163-1.kicad_mod` is still the hypothesis from the abandoned KiCad proposal for TE drawing 776163 (body about 76.8 × 38.8 mm, pin rows at 0 / 4 / 8 mm). Drill and pad sizes are not re-measured against drawing rev K1. Do not fabricate until that drawing is checked.

## Copper

72 segments that ended on the removed Mini-Fit pads were deleted earlier. Header pads still have no tracks. See [ampseal-35-unrouted.md](ampseal-35-unrouted.md).

## Versus stock rusefi/uaefi

Stock uaEFI is a 100 × 100 mm Hellen-One carrier with Mini-Fit harness connectors and corner M3 holes. This board keeps that width, hole pattern, module placement, and rounded-rectangle look, and is 36 mm taller so two AMPSEAL 35 headers can face opposite edges. It is the same family of board, not a copy of the stock outline.
