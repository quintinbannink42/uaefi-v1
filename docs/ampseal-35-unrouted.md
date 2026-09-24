# Header copper

KiCad 8.0.9 refilled the GND zone to the full 100 × 136 mm outline (y 42–178). New tracks were added only where a path stayed clear of other nets. DRC reports **no shorts** and **no crossing tracks**.

These header pads still have no copper connection. A path that meets the 0.15 mm clearance through the Hellen-One modules was not found, so they were left open instead of jumped across other copper:

J30: pin 12 `OUT_INJ6`, pin 15 `OUT_IGN3`, pin 16 `OUT_IGN4`, pin 17 `OUT_IGN5`, pin 18 `OUT_IGN6`, pin 20 `OUT_LS2`, pin 21 `OUT_LS3`, pin 22 `OUT_LS4`, pin 23 `OUT_LS_HOT1`, pin 25 `OUT_DC1+`, pin 26 `OUT_DC1-`, pin 27 `OUT_DC2+`, pin 29 `WBO_Heater`, pin 30 `WBO_Ip`, pin 31 `WBO_Un`, pin 32 `WBO_Vm`, pin 33 `WBO_Rtrim`.

J31: pin 16 `IN_IAT`, pin 18 `IN_FLEX`, pin 19 `IN_KNOCK_RAW`, pin 24 `IN_BUTTON2`, pin 26 `IN_HALL1`, pin 27 `IN_HALL2`, pin 28 `IN_HALL3`, pin 29 `VR_MAX9924+`, pin 30 `VR_MAX9924-`, pin 31 `VR_DISCRETE+`, pin 32 `VR_DISCRETE-`, pin 33 `EGT+`, pin 34 `EGT-`.

Spare pins 34 and 35 on J30 and pin 35 on J31 stay unconnected on purpose. The six nets called out earlier (`OUT_INJ6`, `OUT_DC1+`, `OUT_DC1-`, `OUT_DC2+`, `EGT+`, `EGT-`) are in this open list. They no longer use a direct B.Cu jump.
