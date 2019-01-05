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

### Hardware Info
#### CPU Cooler + RAM Height + Fan Location
The RAM height caused the NH-D15 fan to not fit in the case when exhausting air toward the rear of the case. The included NZXT 3-pin fan at the top had to be moved to the front of the case as an intake. The NH-D15 was then rotated to exhaust air through the top. The fans clips were changed to support this from their original locations to make sure the fans would fit with the graphics card in the fist PCI x16 slot. 

#### NZXT Fans
H500 includes (2) 120mm fans. One is 4-pin and the other is 3-pin. The 4-pin fan runs at a high RPM when in PWM mode. Both NZXT fans run at a lower RPM when calibrated in DC mode from the ASUS BIOS.

## macOS
macOS Mojave version 10.14.2

* Format USB (minimum 8 GB)
* Use Unibeast to create USB installer using the instructions here: https://www.tonymacx86.com/threads/success-gigabyte-designare-z390-thunderbolt-3-i7-9700k-amd-rx-580.267551/

> Now that we have a config that works, it is possible to create a normal USB installer using `createinstallmedia`, install Clover to that USB, then replace the EFI folder on the USB installer with the one here on Github. The boot takes longer, but it works.

## BIOS Settings
* Load optimized defaults
* Auto-configure fans
* Enable Vt-d and Intel (VMX) Virtualization Technology (for VMware Fusion)
* Disabled unused Bluetooth port 3.1-2 (there's a header on the motherboard I'm not using)

## Working
* Mojave install boots successfully
* NVME - Samsung 970 EVO 2TB (~2.5 GB/s WRITE, ~3.1 GB/s READ via BlackMagic Disk Speed Test)
* Radeon RX 580 Displayport output
* Wired Ethernet - Intel I219V7 PCI Express Gigabit Ethernet
* USB 2.0
* Sleep/Wake
* Quicklook
* SATA ports detected, not tested
* S1220 Audio (ALC1220) https://hackintosher.com/guides/get-hackintosh-audio-working/
* Youtube video
* H.264 videos via VLC (.mkv, .m4a, .m4p)
* HWMonitor (after copying required kexts to EFI)
* Wi-Fi
* Bluetooth
* USB-C connect to display - working as a USB hub for additional USB type A ports on display (not confirmed as a display+sound source)

## Not Working
* Charging Macbook via USB-C (It's recognized, but get an error regarding Firewire not being supported on this Mac - 14,2 currently)

## Resources
* Clover https://sourceforge.net/projects/cloverefiboot/
* Clover Configurator https://mackie100projects.altervista.org/download-clover-configurator/
* https://www.tonymacx86.com/threads/success-gigabyte-designare-z390-thunderbolt-3-i7-9700k-amd-rx-580.267551/ This guide got the installer working straight away. I know the board doesn't match, but it works.

## Additional Notes
* Had to apply USBInjectAll.kext for the bluetooth port to be discovered; then disabled it due to something strange with the video card when looking at IORegistryExplorer. I may need to create a custom dsdt, but I don't know how to yet.
* Updating the Product Model/Name from 14,2 to 18,3 required Graphics > Inject ATI. Otherwise, it would boot but not display on local monitor (was able to remote in via Share Screen)
