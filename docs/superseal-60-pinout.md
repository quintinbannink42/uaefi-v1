# SUPERSEAL 1.0 60-pin harness (J30)

One TE **6437288-5** header replaces both AMPSEAL headers (old J30 and J31) and the 2.54 mm 2×02 sockets. Ignition stays smart-coil only. Q7–Q12 stay off the board.

The old AMPSEAL notes are superseded: [ampseal-35-pinout.md](ampseal-35-pinout.md).

## Connector

| | |
|---|---|
| PCB header | TE **6437288-5**, SUPERSEAL 1.0, 60 position, 4 row, 3 mm pitch, right-angle, through-hole, gold, sealable |
| Mating plugs | 34-position **4-1437290-0** (pins 1–34) and 26-position **3-1437290-7** (pins 35–60). Confirm the keying dash against the TE drawing before building a loom. |
| Footprint | `footprints/TE_6437288-5_SuperSeal_60_RA.kicad_mod` |
| Drawing | Hole chart follows the SuperSeal footprint digitized from TE customer drawing **ENG_CD_9-1437287-8** (pad 2.3 mm, drill 1.3 mm, 3.4 mm mounting holes, 38.5 mm section pitch). `JPN_CD_6437288-5` returned HTTP 403 from TE during this pass, so cavity 1 still needs a look at that PDF before a production loom. |

Catalog contact rating is “up to 15 A” by wire. The PCB neck is much lower. See [superseal-60-order.md](superseal-60-order.md).

## What was dropped to fit 60 pins

The previous harness used 67 assigned AMPSEAL pins. No unique signal was dropped. Only paralleled returns were reduced:

| Net | Old parallels | Now | Dropped |
|---|---|---|---|
| GND | 4 | 2 (pins 4 and 5) | 2 |
| +5VP | 3 | 1 (pin 7) | 2 |
| GNDA | 4 | 1 (pin 8) | 3 |

There is no spare pin.

## Pinout

World placement is rotation 270°, pin 1 at (186, 78). Front row (`ly = 0`) is the outer row and leaves toward the right edge. The back row (`ly = 8`) leaves toward the board.

### Front row — power and a few signals

| Pin | Net | Pin | Net |
|---|---|---|---|
| 1 | +12V | 35 | CAN− |
| 2 | +12V_RAW | 36 | EGT+ |
| 3 | 12V_KEY | 37 | EGT− |
| 4 | GND | 38 | VR_MAX9924+ |
| 5 | GND | 39 | VR_MAX9924− |
| 6 | WBO_Heater | 40 | VR_DISCRETE+ |
| 7 | +5VP | 41 | VR_DISCRETE− |
| 8 | GNDA | | |
| 9 | CAN+ | | |

### Outer middle row — sensors

| Pin | Net | Pin | Net |
|---|---|---|---|
| 10 | WBO_Ip | 42 | IN_BUTTON1 |
| 11 | WBO_Un | 43 | IN_BUTTON2 |
| 12 | WBO_Vm | 44 | IN_BUTTON3 |
| 13 | WBO_Rtrim | 45 | IN_HALL1 |
| 14 | IN_MAP | 46 | IN_HALL2 |
| 15 | IN_TPS1 | 47 | IN_HALL3 |
| 16 | IN_TPS2 | | |
| 17 | IN_PPS1 | | |

### Inner middle row — sensors and smart-coil logic

| Pin | Net | Pin | Net |
|---|---|---|---|
| 18 | IN_PPS2 | 48 | OUT_IGN1 |
| 19 | IN_IAT | 49 | OUT_IGN2 |
| 20 | IN_CLT | 50 | OUT_IGN3 |
| 21 | IN_FLEX | 51 | OUT_IGN4 |
| 22 | IN_KNOCK_RAW | 52 | OUT_IGN5 |
| 23 | IN_AUX1 | 53 | OUT_IGN6 |
| 24 | IN_AUX2 | | |
| 25 | IN_AUX3 | | |

### Back row — injectors, DC motor, low-sides

| Pin | Net | Pin | Net |
|---|---|---|---|
| 26 | OUT_INJ1 | 54 | OUT_DC2− |
| 27 | OUT_INJ2 | 55 | OUT_LS1 |
| 28 | OUT_INJ3 | 56 | OUT_LS2 |
| 29 | OUT_INJ4 | 57 | OUT_LS3 |
| 30 | OUT_INJ5 | 58 | OUT_LS4 |
| 31 | OUT_INJ6 | 59 | OUT_LS_HOT1 |
| 32 | OUT_DC1+ | 60 | OUT_LS_HOT2 |
| 33 | OUT_DC1− | | |
| 34 | OUT_DC2+ | | |

## J30 pads still open on the PCB

These header pads are assigned on the schematic and still have a ratsnest break to the rest of the net. Do not treat the harness as electrically complete.

`OUT_DC1+`, `OUT_DC1−`, `OUT_DC2+`, `IN_PPS2`, `CAN−`, `IN_TPS1`, `IN_TPS2`, `IN_BUTTON1`, `IN_BUTTON2`, `IN_BUTTON3`, `IN_HALL1`, `IN_HALL2`, `IN_HALL3`, `IN_MAP`, `WBO_Vm`, `OUT_IGN1`, `OUT_IGN5`, `OUT_IGN6`, `OUT_INJ2`, `OUT_INJ3`, `OUT_INJ5`.

The other 39 pins, including both GND pins, join existing copper. GND uses the plane plus a short stub. Details and current limits: [superseal-60-order.md](superseal-60-order.md).
