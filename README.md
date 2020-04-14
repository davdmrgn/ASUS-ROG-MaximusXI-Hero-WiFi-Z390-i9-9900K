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

### H500 USB

Front panel USB uses 3.0 Gen1 instead of 3.0 Gen2.

### WiFi Adapter Card

PCI card has 3 antennas. The BT/WiFi card only has 2 antenna connections due to its small size (for laptops). Works fine, but a desktop-style card with 3 antenna connections (iMac) could have been used.

According to [this reddit post](https://www.reddit.com/r/hackintosh/comments/an7u0a/inteli99900k32gb_ramvega_64_everything_works/), the [BCM94352Z NGFF 802.11ac Dual Band Wireless WIFI Card Module for Lenovo](https://pcpartpicker.com/product/wmw7YJ/richer-r-wifi-card-bcm94352z-ngff-80211ac-dual-band-wireless-wifi-card-module-for-lenovo-b50-70n50-70b40-80b50-80e40-30e40-70e40-80y40-70y40-80y50-70y50-80y50-70-touchy50-80-touchy-yo) could have worked in the Intel wifi card slot. If that's the case, an ITX board and case could have been used.

## macOS

macOS Catalina version 10.15.3

* Format USB (minimum 8 GB) `diskutil eraseDisk JHFS+ USB /dev/disk#`
* Create a macOS USB installer `sudo /Applications/Install\ macOS\ Catalina.app/Contents/Resources/createinstallmedia --volume /Volumes/USB`

## OpenCore

* [Primary instructions](https://khronokernel-2.gitbook.io/opencore-vanilla-desktop-guide/opencore-efi)
* [EFI mount](https://github.com/corpnewt/MountEFI)
* Mount installer USB EFI
* Copy EFI from OpenCore-0.5.6-DEBUG into USB
* Follow directions on what to remove and what to add
* SSDT details are below
* If changing from Clover to OpenCore, once you're done generating your config.plist, use the same serial number as you did before
* Make sure the model is correct (for this processor, iMac18,3)

### SSDT

SSDT procedures are lengthy and a bit confusing. After doing it, here is my personal summary:

* If you want to do it manually, make an Ubuntu USB installer to generate your DSDT, otherwise, just use/edit the files already available as they appear to have the correct values required
* Only .aml files should be put into the ACPI folder inside the OC\EFI
* Determine which .aml files you'll need based on the primary guide
* A previously configured `SSDT-UIAC.aml` was required to get Bluetooth to work

## BIOS Settings

* [BIOS updated to 1401](https://www.asus.com/Motherboards/ROG-MAXIMUS-XI-HERO-WI-FI/HelpDesk_BIOS/)
  > NOTE: This update broke my original Clover install while on 10.15.3. Reverting to an earlier BIOS (1105) did not work. That's why I'm on OpenCore now.
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

## Post-Install

* Set the Startup disk in macOS system preferences
* Copy USB installer OpenCore EFI to boot disk EFI

## Not Working

## Additional Details

When I upgraded from Mojave to Catalina, it worked but there were changes in Clover which I couldn't confirm. Upgrading my BIOS from 0702 to 1401 caused a boot issue (`Super IODevice: [Fatal] found unsupported chip`). I gave up attempting to fix via Clover and tried OpenCore, which worked on a Catalina installer USB. I used that installer to rename the old EFI folder, then copy the EFI from the Catalina installer USB to my broken Catalina installation (this was done via diskutil in Terminal from the installer).

### Updating OpenCore

Applying updates via Clover was EASY. Doing this in OpenCore is going to be a bit more manual. They suggest keeping a USB of your macOS installer on it, and use that to test OpenCore EFI updates. It's a bit more work than Clover, but everything else seems to be going well.

### Dual Booting Linux (Fix Grub after macOS install)

Linux was installed prior to macOS. Grub was installed to the EFI partition of the Linux disk. OpenCore was installed to the EFI partition of the macOS disk (both OSs were kept separate). After installing macOS, the disk numbering changed which caused the Linux OS to not show up in the ASUS boot menu. This must be repaired using a Linux Live CD.

> NOTE: You cannot boot Linux from OpenCore. Grub reads my Linux disk as `/dev/sdb` or `/dev/hd1` while while OpenCore reads it as `/dev/hd6`. Since the disk numbering between Grub and OpenCore are different, you must boot Linux from the ASUS boot menu.

* Boot to Linux Live CD
* Press CTRL+ALT+T to open a Terminal
* Execute the following commands to
  1. Mount the Linux installation
  2. Bind the supporting mounts from the Live CD into the Linux installation mount
  3. Change root into the Linux installation
  4. Install Grub EFI (this may not be needed as Grub already exists)
  5. Update Grub HD references in the grub.cfg file
  6. Reboot into ASUS boot menu
  7. Boot into Linux (successfully)

```bash
sudo mkdir /mnt
sudo mount /dev/sdb2 /mnt
sudo mount /dev/sdb1 /mnt/efi
sudo mount --bind /dev /mnt/dev
sudo mount --bind /proc /mnt/proc
sudo mount --bind /sys /mnt/sys
sudo chroot /mnt
grub-install --target=x86_64-efi /dev/sdb # may not be needed
grub-install --recheck # may not be needed
update-grub
```

> NOTE: After doing this, I am not able to get into the ASUS BIOS setup - it goes to a black screen. Must completely reset the CMOS using the button on the rear of the motherboard in order to access the BIOS, then restore a saved setting.

> NOTE #2: Prior to resetting the BIOS, there were 2 entries for Linux. After resetting, there is only 1 entry for Linux, which is correct.$$

#### Bluetooth Keyboard and Mouse

1. Pair devices in Linux
2. Pair devices in macOS
3. Log back into iCloud (pairing devices in another OS breaks iCloud integration)
4. Copy macOS bluetooth device keys `sudo defaults read com.apple.bluetoothd.plist LinkKeys` (data after `bytes = 0x`)
5. User PowerShell to convert to uppercase letters
6. Boot into Linux
7. Switch to root `sudo bash`
8. Turn off bluetooth devices
9. Turn off bluetooth in Linux `sudo service bluetooth stop`
10. Edit bluetooth config file `nano /var/lib/bluetooth/D0:81:7A:C7:E7:2F/10:94:BB:9F:4A:90/info`
11. Update Key to the new key from macOS recorded earlier
12. Start bluetooth `sudo service bluetooth start`
13. Monitor bluetooth service `bluetoothctl`
14. Turn on bluetooth device (mouse)
15. Watch it connect and disconnect repeatedly
