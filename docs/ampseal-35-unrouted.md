# Header copper

The board was widened on the right (x 150 → 158 mm) so harness nets could leave the Hellen-One modules on inner layers and in that side channel. KiCad 8 DRC reports **no shorts** and **no crossing tracks**. Every J30/J31 signal pad has a track on its net. Spare pins 34 and 35 on J30 and pin 35 on J31 are still spare.

These required nets are one ratsnest island (header pad reaches the existing onboard copper):

`OUT_INJ6`, `OUT_IGN6`, `OUT_DC1+`, `OUT_DC1-`, `OUT_DC2+`, `WBO_Heater`, `WBO_Vm`, `VR_DISCRETE-`, `EGT+`, `EGT-`.

These required nets still have a single ratsnest break between the new track and an older pad or track of the same net. The header pad is not an open pin; the break is further along the net:

`OUT_IGN3`, `OUT_IGN4`, `OUT_IGN5`, `OUT_LS2`, `OUT_LS3`, `OUT_LS4`, `OUT_LS_HOT1`, `WBO_Ip`, `WBO_Un`, `WBO_Rtrim`, `IN_IAT`, `IN_FLEX`, `IN_KNOCK_RAW`, `IN_BUTTON2`, `IN_HALL1`, `IN_HALL2`, `IN_HALL3`, `VR_MAX9924+`, `VR_MAX9924-`, `VR_DISCRETE+`.

Tracks that shorted or crossed were removed rather than left in. Q7–Q12 stay off the board.
