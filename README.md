# macOS Tahoe 26 on Lenovo IdeaPad Flex 5 14ITL05

**Read the guide online: https://nerdjb.github.io/lenovo-flex5-14itl05-tahoe/**

OpenCore 1.0.8 EFI + documentation for **Lenovo IdeaPad Flex 5 14ITL05 (82HS)**,
i5-1135G7 (Tiger Lake), Intel Iris Xe 80 EU (8086:9A49).

GPU acceleration comes from [JulioNectar/Hackintosh-XPS13Plus-IrisXe-Tahoe]
(Apple's Tiger Lake driver + NootedGreen). This repo is the same stack adapted
to this laptop: different ACPI namespace (PC00, not PCI0), Lenovo embedded
controller, ALC257 audio, ELAN06FA touchpad and WACOM WACF2200 pen/touchscreen.

## What is here

| Path | Contents |
|---|---|
| `EFI/` | bootable OpenCore EFI (installer stage, no NootedGreen) |
| `post-install/` | NootedGreen.kext, AMFIPass.kext, WhateverGreen.kext, instructions |
| `MACOS-TAHOE-GUIDE.html` | full offline guide, 11 sections |

## IMPORTANT - generate your own SMBIOS

The platform identity in this EFI is intentionally **blank**. Before first boot:

1. Windows: open `config.plist` with OCAT, PlatformInfo -> generate for MacBookPro16,2
2. macOS: `./GenSMBIOS` (OpenCorePkg) or OCPT, model `MacBookPro16,2`

Never share your own serial, MLB, SystemUUID or ROM.

## Boot arguments

Installer:
`-v keepsyms=1 debug=0x100 alcid=11 -igfxvesa`

After macOS 26.7.1 + install.sh + NootedGreen + AMFIPass:
`keepsyms=1 debug=0x100 alcid=11 amfi_get_out_of_my_way=1 -allow3d -disablegfxfirmware ngreen-eu=80 ngreen-l3=6`

Do not add `-ngreenpm` / `ngreen-dmc=adlp` / `-ngreentglwithgfx`: those are
Raptor Lake values from the reference machine.

## Known limits

- OpenGL is software-only: macOS Tahoe ships no Tiger Lake OpenGL driver.
- Audio on Tahoe needs SimpleHDA (included); layout 11, try 18/96/97/99/100/101 if wrong.
- Fingerprint (Goodix 27C6:55B4) is not supported.

## Credits

- JulioNectar - NootedGreen, AirportItlwm Tahoe build, macos/ stack
- Acidanthera - OpenCore, Lilu, VirtualSMC, WhateverGreen, AppleALC, NVMeFix, VoodooPS2, BrcmPatchRAM
- VoodooI2C team, OpenIntelWireless, lzhoang2801 (OpCore-Simplify), USBToolBox

No warranty. Flashing firmware or erasing disks can destroy data.

