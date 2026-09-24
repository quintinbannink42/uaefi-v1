# SUPERSEAL 60 mechanical placement

One header, on the right edge. The AMPSEAL pair and the 2.54 mm 2×02 sockets are gone. Modules, USB, J6, J7, and the four M3 holes stay where they were.

Pinout: [superseal-60-pinout.md](superseal-60-pinout.md). Current limits: [superseal-60-order.md](superseal-60-order.md).

## Outline

The outline is **x = 0 to 258, y = 42 to 224** (258 × 182 mm). Corners stay a 3.5 mm radius. The right side holds the header. The left edge (x = 0) and the bottom edge (y = 224) are the routing channel for the wide power and injector tracks. The old 158 × 136 mm outline does not fit that copper.

## J30

| | |
|---|---|
| Reference | J30 |
| Part | TE 6437288-5 |
| Origin | (214, 78), rotation 270° |
| Pin 1 | (214, 78), outer row |
| Pin field | x = 206, 208.5, 211.5, and 214; y = 78–134.5 |
| Mounting holes | 3.4 mm NPTH at x = 199.5, y = 70.75, 109.25, 141.75 |
| Body | catalog envelope about 78 × 36.5 mm, mating height about 27.9 mm |

Rotation 270° points the mating face toward the right edge (x = 258). Confirm the shell against that edge before a panel. Cavity 1 is still unverified.

The 34-position plug (pins 1–34) and the 26-position plug (pins 35–60) sit on either side of the 14.5 mm gap in the pin grid.

## What is not on this board

| Removed | Why |
|---|---|
| J30 and J31 AMPSEAL 35 (776163-1) | Replaced by the single Superseal |
| J1, J11–J22, J24 | 2.54 mm 2×02 sockets (4 pins). These were not the module stackers. |

M1–M7 mezzanine connectors stay. J6, J7, and the USB connectors stay.
