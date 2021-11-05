# ASUS-ROG-MaximusXI-Hero-WiFi-Z390-i9-9900K

This is a log to keep track of my hackintosh config as it is built.

## Parts List

| Type | Item |
| ---- | ---- |
| CPU | [Intel - Core i9-9900K 3.6 GHz 8-Core Processor](https://pcpartpicker.com/product/jHZFf7/intel-core-i9-9900k-36ghz-8-core-processor-bx80684i99900k) |
| CPU Cooler | [Noctua - NH-D15 82.5 CFM CPU Cooler](https://pcpartpicker.com/product/4vzv6h/noctua-cpu-cooler-nhd15) |
| Motherboard | [Asus - ROG MAXIMUS XI HERO (WI-FI) ATX LGA1151 Motherboard](https://pcpartpicker.com/product/zvQG3C/asus-rog-maximus-xi-hero-wi-fi-atx-lga1151-motherboard-rog-maximus-xi-hero-wi-fi) |
| Memory | [Patriot Viper Elite Series DDR4 32GB (2x16GB) 2666MHz PC4-21300 Memory](https://www.amazon.com/gp/product/B079NL4P66/ref=oh_aui_detailpage_o04_s00?ie=UTF8&psc=1) |
| Video Card | [Sapphire - Radeon RX 580 8 GB PULSE Video Card](https://pcpartpicker.com/product/y2DzK8/sapphire-radeon-rx-580-8gb-pulse-video-card-11265-05) |
| Case | [NZXT - H500 (Black) ATX Mid Tower Case](https://pcpartpicker.com/product/p8x2FT/nzxt-h500-black-atx-mid-tower-case-ca-h500b-b1) |
| Power Supply | [EVGA - SuperNOVA G3 550 W 80+ Gold Certified Fully-Modular ATX Power Supply](https://pcpartpicker.com/product/sMM323/evga-supernova-g3-550w-80-gold-certified-fully-modular-atx-power-supply-220-g3-0550) |
| Monitor | [LG - 38WK95C-W 37.5" 3840x1600 60 Hz Monitor](https://pcpartpicker.com/product/XLqhP6/lg-38wk95c-w-375-3840x1600-60hz-monitor-38wk95c-w) |
| Wi-Fi + Bluetooth Adapter PCI-E x1 Card | [WiFi + Bluetooth 4.0 Card to PCI-E x1 Adapter Card PC/Hackintosh Without BCM943224PCIEBT2/bcm94360CS2/BCM943602CS (black)](https://www.amazon.com/gp/product/B076KBBFV4/ref=oh_aui_detailpage_o00_s00?ie=UTF8&psc=1) |
| Wi-Fi Bluetooth Airport Wireless Card | [Padarsey BCM94360CS2 WiFi Bluetooth Airport Wireless Card Compatible for MacBook Air 11" A1465 (2013, 2014, 2015) 13" A1466 (2013, 2014, 2015, 2017) (661-7465, 661-7481, 653-0023)](https://www.amazon.com/gp/product/B07C78VBCD/ref=oh_aui_detailpage_o00_s00?ie=UTF8&psc=1) |

## Hardware Info

- Coffee Lake i9 9900K
- Asus Maximus XI
- Realtek ALC S1220A

### WiFi Adapter Card

PCI card has 3 antennas. The BT/WiFi card only has 2 antenna connections due to its small size (for laptops). Works fine, but a desktop-style card with 3 antenna connections (iMac) could have been used.

According to [this reddit post](https://www.reddit.com/r/hackintosh/comments/an7u0a/inteli99900k32gb_ramvega_64_everything_works/), the [BCM94352Z NGFF 802.11ac Dual Band Wireless WIFI Card Module for Lenovo](https://pcpartpicker.com/product/wmw7YJ/richer-r-wifi-card-bcm94352z-ngff-80211ac-dual-band-wireless-wifi-card-module-for-lenovo-b50-70n50-70b40-80b50-80e40-30e40-70e40-80y40-70y40-80y50-70y50-80y50-70-touchy50-80-touchy-yo) could have worked in the Intel wifi card slot.

## macOS

Monterey 12.0.1

## OpenCore

Version: 0.7.4

- Guide: https://dortania.github.io/OpenCore-Install-Guide/
- Get your installation media
  ```
  cd /Applications/Install\ macOS\ Monterey.app/Contents/Resources
  sudo ./createinstallmedia --volume /Volumes/USB --nointeraction --downloadassets
  ```
- MountEFI: https://github.com/corpnewt/MountEFI
- Setup the OC folder required files:
  - Drivers: 
    - `HfsPlus.efi` for viewing HFS volumes (macOS installers) https://github.com/acidanthera/OcBinaryData/blob/master/Drivers/HfsPlus.efi
    - `OpenCanopy.efi` for graphical boot images
    - `OpenRuntime.efi` to get info for Linux dual boot
  - Kexts:
    - AppleALC (audio) https://github.com/acidanthera/AppleALC/releases
    - Lilu (patches other things) https://github.com/acidanthera/Lilu/releases
    - NVMeFix (storage) https://github.com/acidanthera/NVMeFix/releases
    - VirtualSMC (hardware monitoring) https://github.com/acidanthera/VirtualSMC/releases
      - SMCProcessor
      - SMCSuperIO
    - WhateverGreen (graphics) https://github.com/acidanthera/WhateverGreen/releases
    - USBMap https://github.com/corpnewt/USBMap
- ProperTree https://github.com/corpnewt/ProperTree
- OpenCore Configurator (when you need a GUI)

### ProperTree

- Open `config.plist` in Propertree
- Clean Snapshot (Cmd+Shift+R), select `OC` folder
- Remove `#WARNING` entries
- Coffee Lake specific edits: https://dortania.github.io/OpenCore-Install-Guide/config.plist/coffee-lake.html#starting-point

### USBMap

Rebuilt USBMap.kext during post-install with the following config:

USB Location | Port Name | Type
--- | --- | ---
Case top left (USB header) | HS04/SS08 | 3
Case top right (USB header) | HS03/SS07 | 3
Rear left top | HS05 | 0
Rear left bottom | HS06 | 0
Rear mid top | SS03 | 3
Rear mid bottom | SS04 | 9
Rear right top to bottom | SS05/HS01, SS06/HS02, SS01, SS02 | 3
Internal Broadcom card | HS07 | 2

### SSDT

> NOTE: This section is out of date.

SSDT procedures are lengthy and a bit confusing. After doing it, here is my personal summary:

* If you want to do it manually, make an Ubuntu USB installer to generate your DSDT, otherwise, just use/edit the files already available as they appear to have the correct values required
* Only .aml files should be put into the ACPI folder inside the OC\EFI
* Determine which .aml files you'll need based on the primary guide
* A previously configured `SSDT-UIAC.aml` was required to get Bluetooth to work

## BIOS Settings

> NOTE: This section is out of date.

* [BIOS updated to 1401](https://rog.asus.com/us/motherboards/rog-maximus/rog-maximus-xi-hero-wi-fi-model/helpdesk_bios)
* Reset BIOS by using clear CMOS button on back
* Advanced Mode (F7)
* Load optimized defaults
* Extreme Tweaker\AI Overclock Tuner: Manual
* Extreme Tweaker\CPU Core Ratio: AI Optimized
* Extreme Tweaker\AI Features\Cooler Efficiency Customize: User Specify
* Extreme Tweaker\AI Features\Cooler Score: 175
* Platform Misc\PCI Express Native Power Management: Enable
* Platform Misc\Native ASPM: Enable
* CPU\Intel VMX: Enable
* Advanced\System Agent\VT-d: Enable
* Advanced\Onboard\Intel LAN Controller: Disable
* Advanced\Onboard\LED in working state: All On
* Advanced\Onboard\LED Q-Code: Auto
* Advanced\Onboard\LED in sleep state: Stealth
* Advanced\Onboard\Connectivity mode (Wi-Fi & Bluetooth): Disable
* Advanced\APM\Restore AC Power Loss: Last State
* Advanced\APM\Power on By PCI-E: Enable
* Advanced\PCI\SR-IOV: Enable
* Advanced\USB\XHCI Hand-off: Enable
* Boot\Fast Boot: Disable
* Boot\Wait For F1: Disable
* Boot\Setup Mode: EZ Mode
* Boot\Secure Boot\OS Type: Other OS
* Q-Fan\Set all fans to PWM
* Q-Fan\Optimize All
* Q-Fan\Verify all fans are set to PWM after optimizing
* Q-Fan\Disable unused fans

### ASUS AI Overclocking

AI cooler score of 192 was calculated with the configured fans. The system crashes under load at values of 180+. Manually configuring a cooler score of 175 (38% overclocked) appears to be stable.

## Linux Dual Boot

Dual booting Linux on a separate disk. This was tested using Zorin OS, which has an Ubuntu base which uses GRUB.

> For the purposes of this documentation, the macOS OpenCore disk will be `/dev/sda`, and the Linux disk will be `/dev/sdb`.

- Install macOS and OpenCore to `sda1`
- Before installing Linux, copy/duplicate `/EFI/BOOT/BOOTx64.efi` because Linux will overwrite it with GRUB
- Install Linux to `sda2`, selecting the option of installing the bootloader to `sda2` (even though it won't)
- Boot into Linux, checking if the EFI in `/boot/efi` is mounted to `/dev/sda2` using `lsblk`; if not, edit `/etc/fstab` so Linux mounts the appropriate drive for the Linux EFI in the future
- Boot into macOS using the macOS USB installer
- We need to put all the bootloader files in the right location(s)
  > Remember, Linux overwrote the `BOOTx64.efi` file on `sda1`. So, let's make sure we move that to `sda2` in the appropriate folder(s) and put back the OpenCore `BOOTx64.efi` file so OpenCore/macOS boots.
- Put the Linux GRUB `BOOTx64.efi` file back in `sdb1 /EFI/BOOT` and rename it to `BOOTx64.efi.disabled` to prevent volume `NO NAME` from showing up in OpenCore during boot
- Put the OpenCore `BOOTx64.efi` file back in `sda1 /EFI/BOOT`
- Get the Linux boot disk `PciRoot` information
  - Enable `OpenShell.efi` in OpenCore
  - Boot into OpenShell, find the Linux EFI by checking for the `EFI/ubuntu` folder
    > Hint: Type `FS#:` to change to that disk, `cd` to change directory, and `dir` to view the files
  - Once in the Linux `FS#:` directory, type `map > map-table.txt`, then `exit` and boot back into macOS
> When booting into macOS after being in OpenShell, it sometimes hangs. Hard reset and it should boot into macOS. Once into macOS, clear kext cache by typing `sudo kextcache -i /`. This cleared up any boot delays/issues after being in OpenShell.
- Use OpenCore Configurator to add a boot entry in Misc for the Linux EFI
  - Misc > Boot > Entries > Add
    - Path: Paste in the `PciRoot` string from the `map-table.txt` file of the disk containing the Linux bootloader
    - Add to the end of the path `/\EFI\ubuntu\grubx64.efi`
      > This points to `/dev/sdb1/EFI/ubuntu/grubx64.efi`.
    - Name: `Linux`
    - Enabled: Yes
  - Save the config.plist file

From here, you should be able to boot to Linux from OpenCore, having only 1 boot entry for Linux.

## Issues (and fixes)

- USB HS04@14400000 error at boot
  - Fix: Re-do USBMap.kext
- NVMe kext cache error at boot 
  - Fix: Run `sudo kextcache -i /` in macOS
- ProperTree has black window in Monterey
  - Fix: Install Python, NOT the Universal installer. We need the Intel installer. Forgot where I got it. Generate the ProperTree app and use that. 
- When installing Linux, you tell it to install the bootloader to `/dev/sdb` and it installs to `/dev/sda`. If you happen to have a `/dev/sdc1` it will mount that to `/boot/efi` instead of `/dev/sdb1`.
  - Fix: It's a hot mess. On the first Linux boot, I would check everything before leaving. Make sure the proper devices are mounted and mapped. Use `lsblk` and make sure `fstab` is up to date with the proper volumes IDs. Don't trust it.
