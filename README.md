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

## macOS
macOS Mojave version 10.14.2

* Format USB (minimum 8 GB)
* Use Unibeast to create USB installer using the instructions here: https://www.tonymacx86.com/threads/success-gigabyte-designare-z390-thunderbolt-3-i7-9700k-amd-rx-580.267551/

> Now that I have a config that works, it may be possible to create a normal USB installer using `createinstallmedia`, install Clover to that USB, then copy over any additional kexts and drivers, then copy over the config.plist instead of using Unibeast. _Must test this_

## BIOS Settings
* Load optimized defaults
* Auto-configure fans
* Disable Vt-d

### Post-Installation
* Enable Vt-d and Intel (VMX) Virtualization Technology (for VMware Fusion)

## Working
* Mojave install boots successfully
* NVME - Samsung 970 EVO 2TB
* Radeon RX 580 Displayport output
* Wired Ethernet - Intel I219V7 PCI Express Gigabit Ethernet
* USB 2.0
* Sleep/Wake
* Quicklook
* SATA ports detected, not tested
* S1220 Audio (ALC1220) https://hackintosher.com/guides/get-hackintosh-audio-working/
* Youtube video

## Not Working
* ????

## Not Confirmed
* USB-C
* USB-A 10 Gbps speed
* Video

## Resources
* Clover https://sourceforge.net/projects/cloverefiboot/
* Clover Configurator https://mackie100projects.altervista.org/download-clover-configurator/
* https://www.tonymacx86.com/threads/success-gigabyte-designare-z390-thunderbolt-3-i7-9700k-amd-rx-580.267551/ This guide got the installer working straight away. I know the board doesn't match, but it works.
