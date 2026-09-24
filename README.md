# Ultra Affordable EFI

🟢[$175 base model rusEFI store](https://www.shop.rusefi.com/shop/p/uaefi-ultra-affordable-efi)🟢

## Community Support

🔴Community support ONLY 🔴 https://www.facebook.com/groups/rusEfi 🔴 [Discord](https://github.com/rusefi/rusefi/wiki/Discord)🔴

## Dual AMPSEAL 35 harness (fork)

This fork replaces the Mini-Fit Jr vehicle connectors with two TE AMPSEAL 35-pin headers (J30 and J31, 776163-1 family). See [docs/ampseal-35-pinout.md](docs/ampseal-35-pinout.md). The footprint hole chart is unverified against the current TE drawing. The outline is a taller rounded rectangle in the same family as the uaEFI race core, with J30 on the bottom edge and J31 on the top edge. Nets to those headers are not routed yet ([docs/ampseal-35-mechanical.md](docs/ampseal-35-mechanical.md)).

## Technical Details

Open Source KiCAD 7 hardware powered by [Hellen-One](https://github.com/andreika-git/hellen-one)

powerted by [rusEFI firmware](https://github.com/rusefi/rusefi)

[User Documentation](https://github.com/rusefi/rusefi/wiki/uaEFI)

![x](https://raw.githubusercontent.com/rusefi/uaefi/master/docs/uaefi-a-top.png)

![x](https://raw.githubusercontent.com/rusefi/uaefi/master/docs/uaefi-a-back.png)

## MCU options

1mg of flash is _required_.

One day we shall try https://jlcpcb.com/partdetail/Stmicroelectronics-STM32F427VIT6%2FC57097#EC or https://jlcpcb.com/partdetail/Stmicroelectronics-STM32F437VIT7%2FC1338578#EC

## rusEFI Store

https://www.shop.rusefi.com/shop/p/uaefi-ultra-affordable-efi

## HOWTO JLCPCB

You would need three files from ``boards/uaefi-a/board`` folder to place your JLCPB Assembly order: gerber.zip BOM-JLC.csv and CPL.csv

### Q: Something wrong with BOM?

A: Nope, that's normal nothing to worry about click 'Continue'.

![image](https://github.com/rusefi/uaefi/assets/48498823/1b708b27-13b7-40da-857d-7ef85a8ad960)

### Q: how do I get more RAM for Lua?

A: fabricate with STM32F42xVI firmware would defect extra RAM and give you extra Lua. Once your script does not fit into STM32F42xVI it's F7 time or help us leverage F413.

### Q: I've place an order with JLCPCB and I see scary looking wrong orientation?

A: that's expected. See [boards/uaefi-c/board](boards/uaefi-c/board) ``Original*.png`` files and ``Produce*.png`` after JLCPCB manual review process.