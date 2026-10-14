# SUPERSEAL 60 mechanical placement

One header, on the left edge. The AMPSEAL pair and the 2.54 mm 2×02 sockets are gone. Modules, USB, J6, J7, and the four M3 holes stay on the race-core grid. The header moved; the modules did not.

Pinout: [superseal-60-pinout.md](superseal-60-pinout.md). Current limits: [superseal-60-order.md](superseal-60-order.md).

## Outline

| Board | X | Y | Size |
|---|---|---|---|
| Rev E race core (original uaEFI) | 50–150 | 60–160 | **100 × 100 mm** |
| Right-edge SuperSeal | 0–258 | 42–224 | **258 × 182 mm** |
| Left-edge, header outboard (previous) | 0–151.2 | 52.4–164.5 | **151.2 × 112.1 mm** |
| This layout | 25–150 | 60–160 | **125 × 100 mm** |

Corners stay a 3.5 mm radius.

J30 sits on the original 100 mm core instead of on a 25 mm empty strip. The outline is that core plus the on-board part of the header: x = 25 to 150, y = 60 to 160. The mating shell still hangs off the left edge (x = 25). The header courtyard is x = 25.41 to 49.99, y = 70.45 to 149.04, and it does not overlap U9.

## J30

| | |
|---|---|
| Reference | J30 |
| Part | TE 6437288-5 |
| Origin | (28.2, 138), rotation 90° |
| Pin 1 | (28.2, 138), front row, south end. Silkscreen “1” at (29.4, 140.6) |
| Pin field | x = 28.2, 30.7, 33.7, and 36.2; pin 1 at y = 138, pin 60 at (36.2, 81.5) |
| Mounting holes | 3.4 mm NPTH at x = 42.7, y = 145.25, 106.75, 74.25 |
| Body | catalog envelope about 78 × 36.5 mm. The drawn courtyard is the on-board part; the mating barrel hangs off the left edge (x = 25) |

Rotation 90° points the mating face toward the left edge. Pin 1 is the south end of the front row. Cavity numbers are unchanged from the right-edge placement. World Y order is reversed relative to that placement because the same footprint rotation family puts pin 1 at the south end instead of the north end. Cavity 1 is still unverified.

The 34-position plug (pins 1–34) and the 26-position plug (pins 35–60) sit on either side of the 14.5 mm gap in the pin grid.

## What is not on this board

| Removed | Why |
|---|---|
| J30 and J31 AMPSEAL 35 (776163-1) | Replaced by the single Superseal |
| J1, J11–J22, J24 | 2.54 mm 2×02 sockets (4 pins). These were not the module stackers. |

M1–M7 mezzanine connectors stay. J6, J7, and the USB connectors stay. Q7–Q12 stay off the board.
