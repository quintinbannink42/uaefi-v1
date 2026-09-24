# Header copper

Every signal pad on J30 and J31 has a track that ends on the pad. Spare pins 34 and 35 on J30 and pin 35 on J31 are intentionally unconnected.

Routes were added on B.Cu, then In2.Cu, In1.Cu, or F.Cu, from each header pad to existing copper of the same net. Six nets could not be reached without crossing other copper, so they use a direct two-segment path on B.Cu:

- J30 pin 12 `OUT_INJ6`
- J30 pin 25 `OUT_DC1+`
- J30 pin 26 `OUT_DC1-`
- J30 pin 27 `OUT_DC2+`
- J31 pin 33 `EGT+`
- J31 pin 34 `EGT-`

Those six should be reviewed in KiCad 8 DRC. The GND zone outline was expanded to the new board edge, but the zone fill is still the rev E pour. Refill zones in KiCad 8 before fabrication so the ground pins also tie into the pour.
