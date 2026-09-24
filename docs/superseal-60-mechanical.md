# SUPERSEAL 60 mechanical placement

One header, on the right edge. The AMPSEAL pair and the 2.54 mm 2×02 sockets are gone. Modules, USB, J6, J7, and the four M3 holes stay where they were.

Pinout: [superseal-60-pinout.md](superseal-60-pinout.md). Current limits: [superseal-60-order.md](superseal-60-order.md).

## Outline

The old right edge was x = 158. It is now **x = 208**, so the board is 158 × 136 mm instead of 108 × 136 mm. Corners stay a 3.5 mm radius. The extra 50 mm is empty copper area for the header and its fanout. Top and bottom edges are unchanged (y = 42 and y = 178).

## J30

| | |
|---|---|
| Reference | J30 |
| Part | TE 6437288-5 |
| Origin | (186, 78), rotation 270° |
| Pin 1 | (186, 78), outer row, toward the right edge |
| Pin field | about x = 178–186, y = 78–134.5 |
| Mounting holes | 3.4 mm NPTH at x = 171.5, y ≈ 70.8, 109.3, 141.8 |
| Body | catalog envelope about 78 × 36.5 mm, mating height about 27.9 mm |

Rotation 270° points the mating face at the right edge. The shell hangs off x = 208. That is intentional.

The 34-position plug (pins 1–34) and the 26-position plug (pins 35–60) sit on either side of the 14.5 mm gap in the pin grid.

## What is not on this board

| Removed | Why |
|---|---|
| J30 and J31 AMPSEAL 35 (776163-1) | Replaced by the single Superseal |
| J1, J11–J22, J24 | 2.54 mm 2×02 sockets (4 pins). These were not the module stackers. |

M1–M7 mezzanine connectors stay. J6, J7, and the USB connectors stay.
