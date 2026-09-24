# Header copper

The board is 108 × 136 mm (x 50–158 mm, y 42–178 mm). The right 8 mm is a routing channel. KiCad 8 DRC reports **no shorts** and **no crossing tracks**.

Every required J30/J31 signal net is one ratsnest island from the header through to the existing module and onboard copper:

`OUT_INJ6`, `OUT_IGN6`, `OUT_DC1+`, `OUT_DC1-`, `OUT_DC2+`, `WBO_Heater`, `WBO_Vm`, `VR_DISCRETE-`, `EGT+`, `EGT-`, `OUT_IGN3`, `OUT_IGN4`, `OUT_IGN5`, `OUT_LS2`, `OUT_LS3`, `OUT_LS4`, `OUT_LS_HOT1`, `WBO_Ip`, `WBO_Un`, `WBO_Rtrim`, `IN_IAT`, `IN_FLEX`, `IN_KNOCK_RAW`, `IN_BUTTON2`, `IN_HALL1`, `IN_HALL2`, `IN_HALL3`, `VR_MAX9924+`, `VR_MAX9924-`, `VR_DISCRETE+`.

Spare pins 34 and 35 on J30 and pin 35 on J31 are still spare. Q7–Q12 stay off the board.
