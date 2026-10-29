# SUPERSEAL 60 mechanical placement

One header, on the north edge, mating face off the board. The AMPSEAL pair, the 2.54 mm 2×02 sockets, and the prototyping hole grids are gone. Modules, USB, J6, J7, and the four M3 holes stay on the race-core grid.

Pinout: [superseal-60-pinout.md](superseal-60-pinout.md). Current limits: [superseal-60-order.md](superseal-60-order.md).

## Outline

| Board | X | Y | Size |
|---|---|---|---|
| Rev E race core (original uaEFI) | 50–150 | 60–160 | **100 × 100 mm** |
| Right-edge SuperSeal | 0–258 | 42–224 | **258 × 182 mm** |
| Left-edge, header outboard (previous) | 0–151.2 | 52.4–164.5 | **151.2 × 112.1 mm** |
| This layout | 49–150 | 44.8–160 | **101.0 × 115.2 mm** |

Corners stay a 3.5 mm radius.

The left edge is back at the race core. The extra 15.2 mm is the on-board depth of J30 on the north side. The shroud opening hangs off y = 44.8, so the plug is inserted from outside the board.

## J30

| | |
|---|---|
| Reference | J30 |
| Part | TE 6437288-5 |
| Origin | (128.25, 62), rotation 180° |
| Pin 1 | (128.25, 62), front row, on the board side of the field |
| Mating face | local +Y of the footprint, which rotation 180° sends to decreasing world Y, off the north edge |
| Mounting holes | 3.4 mm NPTH at y = 47.5, x = 64.5, 97.0, 135.5, on the board |
| Body | catalog envelope about 78 × 36.5 mm. The drawn shroud reaches about y = 40.2 and crosses the north edge |

Rotation 90° on the left edge pointed that same shroud into the board. Rotation 180° turns it around. The footprint has no 3D model attached; the mating direction is the shroud drawn on local +Y (silk y = 10.2 to 20.5, mounting holes at local y = 14.5). Cavity numbers are unchanged. Cavity 1 is still unverified.

## Prototyping grids removed

`G3` and `G4` (`PROTO_AREA`, 2.54 mm) and the loose holes `P1`, `P2`, `P5`, `P6`, plus the silk labels `3.3`, `5`, `12`, `G`, `H`, `L`, `CAN2`, and `VR 9924 DISCR`. Single test pads that are not part of that grid stay (`P3`, `P4`, `P7`, `P8`, `P15`–`P18`).

The 34-position plug (pins 1–34) and the 26-position plug (pins 35–60) sit on either side of the 14.5 mm gap in the pin grid.

## What is not on this board

| Removed | Why |
|---|---|
| J30 and J31 AMPSEAL 35 (776163-1) | Replaced by the single Superseal |
| J1, J11–J22, J24 | 2.54 mm 2×02 sockets (4 pins). These were not the module stackers. |

M1–M7 mezzanine connectors stay. J6, J7, and the USB connectors stay. Q7–Q12 stay off the board.
