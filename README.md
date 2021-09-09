# Opencore-i9-9900K-Z390-Designare-RX-6800XT
Hackintosh - Opencore 0.7.x EFI, Big Sur, Intel i9 9900K, Z390 Designare, Radeon RX 6800 XT

* Opencore 0.7.2
* Big Sur 11.5.2

## Disclaimer

These files have been created for my specific build. If you have the exact same machine they should work for you too but use at your own risk. If your setup varies I don't recommend using as is, but you may find useful as a reference.

I recommend before copying any EFI folders do your research and understand how Opencore works. Yes, it's not quick or particulalrly easy but is the best way of maintaining a hackintosh.

### My build

This is a dual boot machine that current runs Windows 10 as well as Mac OS Big Sur.

### The two main purposes for this build:

1. Powerful daily driver for Photoshop, InDesign, Premier and Blender on Mac
1. Windows gaming rig

The main build is listed here, the optional extras are mainly lots of drives for storage and backups.

* Z390 Designare F9i firmware (Only update to F9i DO NOT update to f9j).
* Intel i9-9900k 3.6GHz
* 2 x 16GB Vengeance LPX 3200MHz
* ASUS TUF RX 6800 XT OC
* Samsung 970 EVO Plus 970 512GB
* Asus USB-BT400 Bluetooth dongle
* TP-Link Archer T9E AC1900 WiFi card
* Corsair Hydro H150i Pro
* EVGA SuperNova 750 G3
* Fractal Define S2 case

#### Optional extras

* 9 pin USB header male 1 to 4 female extension (to control RGB on CPU cooler)
* ADATA XPG SX8200 Pro 1TB (Mac storage)
* ADATA XPG SX8200 Pro 1TB (Windows 10)
* WD WD10EZEX 1TB HDD (Backup drive Mac OS)
* WD WD10EZEX 1TB HDD (Backup drive Mac storage)
* WD Black 2TB HDD (Windows Games storage)
* Startech M.2 PCIe SSD Adapter (to enable more M.2 drives to be used)
* BenQ PD3200U 32" 4K Designer monitor
* Logitech MX Master 3 wireless mouse
* Logitech MX Keys wireless keyboard

#### How I've configured my drives (optional)

1. 512GB M.2 SSD Mac OS (system only)
1. 1TB M.2 SSD Mac storage (Move 'users' from Mac OS drive to this drive via System Preferences > Users & Groups)
1. 1TB M.2 SSD Windows 10
1. 1TB M.2 SSD Mac OS backup
1. 1TB M.2 SSD Mac Storage backup
1. 1TB HDD Windows 10 backup
1. 2TB HDD Windows (Games storage)

Keeping Mac OS separate from Mac storage helps protect storage during OS updates.

#### Before carrying out an update:

  1. Back up drives using Carbon Copy Cloner or similar
  1. Move 'Users' back to Mac OS drive (keep a copy on Mac Storage)
  1. Check for latest Kext files
  1. After successful update move 'Users' back to Mac storage drive

Keeping a backup of Mac OS and importanly a stable EFI means you'll always be able boot into your backup should an update on your primary Mac OS drive fail (remember to clean NVRAM and then change boot drive in BIOS to boot in to backup).

Once you've successfully updated your main Mac OS drive and tested it's working, copy the drive over to your backup and remember to also copy over your latest EFI.

The other drives listed are for Windows.

### Multiboot

There are a couple of options for multiboot. It's possible to setup Bootcamp to run Windows but I prefer to keep the two completely separate.

Before installing Mac OS I first installed Windows. Once complete then installed Mac OS via a Boot drive USB.

To ensure Windows doesn't corrupt the Mac OS EFI, it's possible to cache (and protect from being cleared) bootx64.efi in to NVRAM allowing the bootx64.efi file to be removed from the EFI folder.

More info on Launcher Option https://dortania.github.io/OpenCore-Post-Install/multiboot/bootstrap.html#prerequisites

If you want to boot in to Mac OS by default, go to System Preferences > Startup Disk and select the Mac OS boot drive. On restart OC should have Mac selected by default.

### EFI includes

#### ACPI

I've tried to keep this as vanilla as possible using manually created SSDT files specific to the Z390 Designare motherboard. I've also used some of the SSDTs recommended in the CaseySJ build guide https://www.tonymacx86.com/threads/success-gigabyte-designare-z390-thunderbolt-3-i7-9700k-amd-rx-580.267551/

* SSDT-DMAC.aml
* SSDT-DMAR.aml
* SSDT-DTPG.aml
* SSDT-EC.aml
* SSDT-PLUG.aml
* SSDT-RTC0.aml
* SSDT-TB3-HackinDROM.aml
* SSDT-UIAC-DESIGNARE-Z390-V7.aml
* SSDT-Z390-DESIGNARE-TB3HP.aml

#### Drivers

* AudioDxe.efi
* HfsPlus.efi
* OpenCanopy.efi
* OpenRuntime.efi

#### Kexts

* AppleALC.kext
* IntelMausi.kext
* Lilu.kext
* SmallTreeIntel82576.kext
* SMCProcessor.kext
* SMCSuperIO.kext
* USBPorts.kext
* VirtualSMC.kext
* WhateverGreen.kext

### A word about USB Ports

The included USBPorts.kext is mapped to the Z390 Designare. Almost all ports work, however I use a splitter from the USB header on the mobo to control the Corsair cooler RGB. This causes sleep issues for the 2 USB2.0 ports on the case front IO panel. I found that with them enabled Mac OS would sleep and then wake a few seconds later, these ports have been disabled.

### Pre install

If you already have a working Hackintosh, back up everything, the drive, EFI etc.

If this is a fresh install or an upgrade from Catalina create a boot installer and place this EFI on the boot installer USB.

### Install

When booting from boot installer USB make sure if you're upgrading that you clear NVRAM.
In BIOS ensure you are booting from boot installer USB.
From OC boot menu select the boot installer USB

This should go through the install process. If the screen goes blank and even if the monitor goes in to standby leave for a few mintues. The first time I installed this I thought it had failed. You should then see the Apple logo and a countdown.
Installer will then reboot and it should then preselect 'Install Mac OS' (or similar) from OC boot menu.
Install will continue, it can take a while so grab a drink and snacks.

### Post Install

Mount your Mac SSD/HDD and boot USB, copy the EFI to your Mac SSD/HDD and restart.
In BIOS change boot drives to only Mac volume, disable all others.
Install Monitor Control for volume control https://github.com/MonitorControl/MonitorControl

### What's working

Overall the build is stable and from what I can see is pretty much a 'golden' build. There are some very minor bugs but these seem more related to general hackintosh/hardware limitations rather than OC/config issues. 

* NVRAM
* USB Ports
* Thunderbolt (partial, full functionality requires flashing firmware. I have no TB hardware and therefore isn't something I'm not concerned with)
* WiFi
* Ethernet (both ports work with SmallTreeIntel82576.kext)
* Bluetooth
* iGPU/Hardware accelleration
* AppleVTD
* Multiboot
* Sleep/Wake
* Boot GUI (Syrah)
* Volume (using Monitor Control and Sound Control)
* iMessages
* iCloud
* Boot chime (Limitation: can only work via audio output and digital audio output, not via HDMI/Displayport)

### DRM

If DRM support in Safari (for Netflix etc) is important to you change SMBIOS to MacPro1,1. Doing so however, you will lose iGPU/Hardware accelleration (useful for Final Cut Pro etc) which I consider to be useful. 

### Bugs

Bluetooth audio is a bit flakey

### Changelog

#### 02/09/2021

* Opencore 0.7.2
* Mac OS Big Sur 11.5.2


