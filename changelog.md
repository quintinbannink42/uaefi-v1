# Dual AMPSEAL harness (this fork)

* External Mini-Fit harness connectors J2, J3, J4, J5, and J10 are replaced by two TE AMPSEAL 35-pin headers J30 (outputs / power / WBO) and J31 (sensors / CAN).
* Pinout: [docs/ampseal-35-pinout.md](docs/ampseal-35-pinout.md).
* Footprint `kicad6-libraries/TE_AMPSEAL_35_776163-1.kicad_mod` is a hypothesis adapted from a public KiCad proposal; verify against TE drawing 776163 before fabrication.
* Board copper is not re-routed. One paralleled `+5VP` and one paralleled `GNDA` pin were dropped to fit 70 positions.
* Outline is a 100 × 136 mm rounded rectangle. J30 is on the bottom edge and J31 is on the top edge. See [docs/ampseal-35-mechanical.md](docs/ampseal-35-mechanical.md).
* Dumb-coil IGBTs Q7–Q12 are removed. Ignition is smart-coil only.
* Header pads are tracked to existing nets. Order notes: [docs/ampseal-35-order.md](docs/ampseal-35-order.md). Refill zones and run DRC in KiCad 8 before fabrication.

# rev E

* power supply fix for RTC
* https://github.com/rusefi/uaefi/issues?q=state%3Aopen%20label%3A%22rev-E%22

# rev D

August 2024

* logic analyzer hookup points for both VRs #66
* minor silkscreen improvements https://github.com/rusefi/uaefi/issues?q=label%3Arev-D+is%3Aclosed

# rev C

Apr 2024

* pad for resistor between VR lines
* a few silkscreen corrections
* full list https://github.com/rusefi/uaefi/issues?q=label%3Arev-C+is%3Aclosed

# rev B

Feb 2024

* [over-current protection on all low side outputs](https://github.com/rusefi/uaefi/issues/44)
* [over-current protection on ignition outputs](https://github.com/rusefi/uaefi/issues/42)
* 0805 button input pull-up/pull-downs added
* button inputs changed from 10K PU to 680K PD https://github.com/rusefi/uaefi/issues/36
* minor cosmetic https://github.com/rusefi/uaefi/labels/rev-B

# rev A

Dec 2023

It works it's great!
