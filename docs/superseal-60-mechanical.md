# SUPERSEAL 60 mechanical placement

One header, on the left edge. The AMPSEAL pair and the 2.54 mm 2×02 sockets are gone. Modules, USB, J6, J7, and the four M3 holes stay on the race-core grid. The header moved; the modules did not.

Pinout: [superseal-60-pinout.md](superseal-60-pinout.md). Current limits: [superseal-60-order.md](superseal-60-order.md).

## Outline

| Board | X | Y | Size |
|---|---|---|---|
| Rev E race core (original uaEFI) | 50–150 | 60–160 | **100 × 100 mm** |
| Right-edge SuperSeal (previous) | 0–258 | 42–224 | **258 × 182 mm** |
| This layout | 0–151.2 | 52.4–164.5 | **151.2 × 112.1 mm** |

Corners stay a 3.5 mm radius.

The right-edge board grew to 258 mm so the header at x = 214 could face +X and the wide nets had a channel. That growth is gone. J30 now faces the left edge, and the outline is the copper extent of this route: x = 0 to 151.2, y = 52.4 to 164.5.

The header courtyard itself is 24.6 mm deep (x = 0.73 to 25.28). Set against the original 100 mm core, that would be a 124.6 mm board. The routed board is wider because the escape from the 60-pin field occupies about x = 26–50, outboard of U9–U11 and the power devices. Sliding the header onto that copper, or sliding the core onto the header, crossed harness tracks and shorted module pads, so the outline was not closed past the escape channel. The extra height versus 100 mm is the same cause: the original top and bottom edges are already filled (mounting holes and module copper), and the header nets run just outside them.

## J30

| | |
|---|---|
| Reference | J30 |
| Part | TE 6437288-5 |
| Origin | (3.5, 138), rotation 90° |
| Pin 1 | (3.5, 138), front row, south end |
| Pin field | x = 3.5, 6.0, 9.0, and 11.5; pin 1 at y = 138, pin 60 at (11.5, 81.5) |
| Mounting holes | 3.4 mm NPTH at x = 18.0, y = 145.25, 106.75, 74.25 |
| Body | catalog envelope about 78 × 36.5 mm. The drawn courtyard is the on-board part; the mating barrel hangs off the left edge (x = 0) |

Rotation 90° points the mating face toward the left edge. Pin 1 is the south end of the front row. Cavity numbers are unchanged from the right-edge placement. World Y order is reversed relative to that placement because the same footprint rotation family puts pin 1 at the south end instead of the north end. Cavity 1 is still unverified.

The 34-position plug (pins 1–34) and the 26-position plug (pins 35–60) sit on either side of the 14.5 mm gap in the pin grid.

## What is not on this board

| Removed | Why |
|---|---|
| J30 and J31 AMPSEAL 35 (776163-1) | Replaced by the single Superseal |
| J1, J11–J22, J24 | 2.54 mm 2×02 sockets (4 pins). These were not the module stackers. |

M1–M7 mezzanine connectors stay. J6, J7, and the USB connectors stay. Q7–Q12 stay off the board.
