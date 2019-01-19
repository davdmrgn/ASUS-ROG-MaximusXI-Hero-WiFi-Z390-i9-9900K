# ASUS-ROG-MaximusXI-Hero-WiFi-Z390-i9-9900K
This is a log to keep track of my hackintosh config as it is built.

## Parts List
Type|Item
:----|:----
**CPU** | [Intel - Core i9-9900K 3.6 GHz 8-Core Processor](https://pcpartpicker.com/product/jHZFf7/intel-core-i9-9900k-36ghz-8-core-processor-bx80684i99900k)
**CPU Cooler** | [Noctua - NH-D15 82.5 CFM CPU Cooler](https://pcpartpicker.com/product/4vzv6h/noctua-cpu-cooler-nhd15)
**Motherboard** | [Asus - ROG MAXIMUS XI HERO (WI-FI) ATX LGA1151 Motherboard](https://pcpartpicker.com/product/zvQG3C/asus-rog-maximus-xi-hero-wi-fi-atx-lga1151-motherboard-rog-maximus-xi-hero-wi-fi)
**Memory** | [Patriot Viper Elite Series DDR4 32GB (2x16GB) 2666MHz PC4-21300 Memory](https://www.amazon.com/gp/product/B079NL4P66/ref=oh_aui_detailpage_o04_s00?ie=UTF8&psc=1)
**Video Card** | [Sapphire - Radeon RX 580 8 GB PULSE Video Card](https://pcpartpicker.com/product/y2DzK8/sapphire-radeon-rx-580-8gb-pulse-video-card-11265-05)
**Case** | [NZXT - H500 (Black) ATX Mid Tower Case](https://pcpartpicker.com/product/p8x2FT/nzxt-h500-black-atx-mid-tower-case-ca-h500b-b1)
**Power Supply** | [EVGA - SuperNOVA G3 550 W 80+ Gold Certified Fully-Modular ATX Power Supply](https://pcpartpicker.com/product/sMM323/evga-supernova-g3-550w-80-gold-certified-fully-modular-atx-power-supply-220-g3-0550)
**Monitor** | [LG - 38WK95C-W 37.5" 3840x1600 60 Hz Monitor](https://pcpartpicker.com/product/XLqhP6/lg-38wk95c-w-375-3840x1600-60hz-monitor-38wk95c-w)
**Wi-Fi + Bluetooth Adapter PCI-E x1 Card** | [WiFi + Bluetooth 4.0 Card to PCI-E x1 Adapter Card PC/Hackintosh Without BCM943224PCIEBT2/bcm94360CS2/BCM943602CS (black)](https://www.amazon.com/gp/product/B076KBBFV4/ref=oh_aui_detailpage_o00_s00?ie=UTF8&psc=1)
**Wi-Fi Bluetooth Airport Wireless Card** | [Padarsey BCM94360CS2 WiFi Bluetooth Airport Wireless Card Compatible for MacBook Air 11" A1465 (2013, 2014, 2015) 13" A1466 (2013, 2014, 2015, 2017) (661-7465, 661-7481, 653-0023)](https://www.amazon.com/gp/product/B07C78VBCD/ref=oh_aui_detailpage_o00_s00?ie=UTF8&psc=1)

## Hardware Info
### CPU Cooler + RAM Height + Fan Location
The RAM height caused the NH-D15 fan to not fit in the case when exhausting air toward the rear of the case. NH-D15 installation is possible when venting through the top of the case (vertical) instead of the rear (horizontal). In this configuration, the video card may need to be positioned in the middle x16 PCI slot (not ideal).

### Fan Situation
Location|Fan|Size|RPM|dbA|m3/h
:----|:----|:----|:----|:----|:----
CPU Cooler (NH-D15) | NF-A15 PWM | 140mm | 300-1200 | 19.2 | 115.5
CPU Cooler (NH-D15) | NF-A12x25 PWM | 120mm | 450-2000 | 22.6 | 102.1
Rear (Exhaust) | NF-A12x25 PWM | 120mm | 450-2000 | 22.6 | 102.1
Top Rear (Exhaust) | NF-A15 PWM | 140mm | 300-1200 | 19.2 | 115.5
Front (Intake) | (2) NF-A14 PWM | 140mm | 300-1500 | 24.6 | 115.5

### Asus Fan Curve Settings
Fan|Low Temp|Mid Temp|High Temp|Ramp Up|Ramp Down|Source|Auto-Stop
:----|:----|:----|:----|:----|:----|:----|:----
CPU (Cooler)|20% @ 40C|60% @ 60C|Not Used|0s|5s|CPU|
H-AMP Fan (Top)|20% @ 40C|60% @ 60C|Not Used|12s|25s|CPU|Yes
Cassis Fan 1 (Rear)|20% @ 40C|60% @ 60C|Not Used|12s|25s|CPU|
Cassis Fan 2 (Front Top)|25% @ 40C|60% @ 60C|Not Used|12s|25s|CPU+Mobo|
Cassis Fan 3 (Front Bottom)|25% @ 40C|60% @ 60C|Not Used|12s|25s|CPU|

### NZXT Fans
H500 includes (2) 120mm 3-pin fans. Not used in this build.

### H500 USB
Front panel USB uses 3.0 Gen1 instead of 3.0 Gen2.

### WiFi Adapter Card
PCI card has 3 antennas. The BT/WiFi card only has 2 antenna connections due to its small size (for laptops). Works fine, but a desktop-style card with 3 antenna connections (iMac) could have been used.

## macOS
macOS Mojave version 10.14.2
* Format USB (minimum 8 GB) `diskutil eraseDisk JHFS+ USB /dev/disk#`
> The above command was required for a USB drive which did not have an EFI partition, not created with the GUID partition scheme. The option to create the GUID partition scheme was not in the Mojave Disk Utility GUI.

* Create a macOS USB installer `sudo /Applications/Install\ macOS\ Mojave.app/Contents/Resources/createinstallmedia --volume /Volumes/USB`
* Install Clover to USB installer
* Run Clover Configurator to create/update EFI partition, or copy EFI folder here to the EFI partition

## BIOS Settings
* Load optimized defaults
* Optimize fans
* Set fan curve to standard
* Enable Vt-d (for VMware Fusion)
* Enable Intel (VMX) Virtualization Technology (for VMware Fusion)
* XHCI Hand-off: Enabled
* Advanced\System Agent (SA) Configuration\Graphics Configuration
    * Primary Display: PCIE
    * iGPU Multi-Monitor: Enabled (required for JPEG preview/quick look)

### Asus AI Overclocking
A cooler score of 192 was calculated with the configured fans. The system crashes in Windows under load at values of 180+. Manually configuring a cooler score of 175 (38% overclocked) appears to be stable.

## Working
* Mojave install boots successfully
* NVME - Samsung 970 EVO 2TB (~2.5 GB/s WRITE, ~3.1 GB/s READ via BlackMagic Disk Speed Test)
* Radeon RX 580 Displayport output
* Wired Ethernet - Intel I219V7 PCI Express Gigabit Ethernet
* USB 2.0
* Sleep/Wake
* Quicklook
* S1220 Audio (ALC1220) https://hackintosher.com/guides/get-hackintosh-audio-working/
* Youtube video
* H.264 videos via VLC (.mkv, .m4a, .m4p)
* HWMonitor (after copying required kexts to EFI)
* Wi-Fi
* Bluetooth
* USB-C connect to display - working as a USB hub for additional USB type A ports on display (not confirmed as a display+sound source)

## Not Working
* Charging Macbook via USB-C (It's recognized, but get an error regarding Firewire not being supported on this Mac - 14,2 at the time of testing)
* Front audio jacks

## Resources
* [Clover](https://sourceforge.net/projects/cloverefiboot/)
* [Clover Configurator](https://mackie100projects.altervista.org/download-clover-configurator/)
* [This guide](https://www.tonymacx86.com/threads/success-gigabyte-designare-z390-thunderbolt-3-i7-9700k-amd-rx-580.267551/) got the installer working straight away. I know the board doesn't match, but it worked.
* [Hardware sensors and fan speed](https://hackintosher.com/guides/hwmonitor-hackintosh-guide/)
    * [RehabMan's FakeSMC](https://bitbucket.org/RehabMan/os-x-fakesmc-kozlek/downloads/)
* [Guide to Fresh Installing Mojave](https://hackintosher.com/guides/guide-to-fresh-installing-macos-mojave-on-a-hackintosh-10-14/)
* [Mojave Update](https://hackintosher.com/guides/updating-your-hackintosh-to-mojave-10-14)

## SSDT (USB)
In this configuration, the 2 rear black USB ports, USB 3.0 Gen2 motherboard header, and one of the USB 2.0 headers are not enabled in order to stay within macOS's 15-port limit.
* Make sure `USBInjectAll.kext` and USB port limit patch is applied is applied
* Open About This Mac > System Report > Hardware > USB
* Take note of the USB 3.1 Bus PCI Device ID (0xa36d)
* Open SSDT-UIAC-ALL.dsl in MaciASL
* Find the section which matches the above PCI Device ID, and remove all other sections
* The current SSDT-UIAC file is configured as follows:
    * HS01: Asus Aura Lighting - DISABLED
    * HS02: USB 3.1 Gen 2 front panel connector (U31G2_2) - DISABLED
    * HS03: USB 3.1 Gen 2 rear - ENABLED
    * HS04: USB 3.1 Gen 2 rear - ENABLED
    * HS05: USB 3.1 Gen 2 rear - ENABLED
    * HS06: USB-C 3.1 rear - ENABLED
    * HS07: USB 3.1 Gen 1 rear - ENABLED
    * HS08: USB 3.1 Gen 1 rear - ENABLED
    * HS09: USB 3.1 Gen 1 front - ENABLED
    * HS10: USB 3.1 Gen 1 front - ENABLED
    * HS11: USB 2.0 rear - DISABLED
    * HS12: USB 2.0 rear (BIOS Flashback) - DISABLED
    * HS13: USB 2.0 connector USB_E12 - ENABLED (Used for Broadcom bluetooth PCI adapter)
    * HS14: USB 2.0 connector USB_E34 - DISABLED
    * SS03: ENABLED
    * SS04: ENABLED
    * SS05: ENABLED
    * SS06: USB-C 3.1 rear - High Speed USB ENABLED
    * SS09: ENABLED
    * SS10: ENABLED
    * Other Super Speed (SS) USB ports are DISABLED 
* Save as `SSDT-UIAC-ALL.aml` file to `EFI/CLOVER/ACPI/patched/`
* Disable USB port limit patch

## Clover Files
Kext | Usage
--- | ---
AppleALC.kext | Audio
FakeSMC.kext | Required
FakeSMC_ACPISensors.kext | HWMonitor
FakeSMC_CPUSensors.kext | HWMonitor
FakeSMC_GPUSensors.kext | HWMonitor
FakeSMC_LPCSensors.kext | HWMonitor
FakeSMC_SMMSensors.kext | HWMonitor
IntelMausiEthernet.kext | Ethernet
Lilu.kext | Audio + Graphics
USBInjectAll.kext | USB
WhateverGreen.kext | Graphics

## Update System Info CPU
* https://www.insanelymac.com/forum/topic/323469-change-cpu-name-in-about-this-mac/?do=findComment&comment=2488294

Updated file [./AppleSystemInfo.strings](here)

## Additional Notes
* Updating the Product Model/Name from 14,2 to 18,3 required Graphics > Inject ATI. Otherwise, it would boot but not display on local monitor (was able to remote in via Share Screen). Using Lilu.kext and WhateverGreen.kext is a replacement for Inject ATI in Clover.
* macOS will not sleep when LG display is set to Deep Sleep Mode
