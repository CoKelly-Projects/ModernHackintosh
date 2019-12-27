# Modern Hackintosh Guide

## DISCLAIMER

I am not responsible for any damage caused to your components, data loss, or anything else that may happen throughout this process. Follow this guide at your own risk! The steps listed below worked for my components. You will find my components under the [My Build Components](#my-build-components) section. There is no guarantee this guide will work for your components. You are responsible for reading about and knowing the guides, documentation, and programs lsited below. The steps within this guide are for AMD based components, however there are links within [Resources](#resources) that have steps for Intel and NVIDIA based components. Without further ado, good luck and ask questions!

## Table of Content

1. [Resources](#resources)
2. [Credit](#credit)
3. [Build Components](#my-build-components)
4. [Getting Started](#getting-started)
5. [Dowloading Catalina](#downloading-catalina)
6. [Creating the USB](#creating-the-usb)
7. [Installing OpenCore](#installing-opencore)
8. [Adding KEXTs, Drivers, and ACPIs](#adding-kexts-drivers-and-acpis)
9. [Configuring config.plist](#configuring-plist)
10. [First Boot](#first-boot)
11. [Formatting SSD](#formatting-ssd)
12. [Finishing the Installation](#finish-installation)
13. [Adding Clover to the SSD](#adding-clover-to-the-ssd)
14. [Generating the SMBIOS](#generating-the-smbios)
15. [Setting up Apple Accounts](#setting-up-apple-accounts)
16. [Benchmarks](#benchmarks)
17. [Footnotes](#footnotes)

## Resources

Reddit: https://www.reddit.com/r/hackintosh/

AMD OSX Forum: https://forum.amd-osx.com/

AMD Vanilla Install Guide: https://vanilla.amd-osx.com/

gibMacOS: https://github.com/corpnewt/gibMacOS

OpenCore: https://github.com/acidanthera/OpenCorePkg/releases

OpenCore Vanilla Guide: https://khronokernel-2.gitbook.io/opencore-vanilla-desktop-guide/

KEXTs: https://onedrive.live.com/?cid=fe4038da929bfb23&id=FE4038DA929BFB23%21455036&authkey=%21APjCyRpzoAKp4xs

## Credit

* Reddit
  * r/SlackyHacky
  * r/dj_chapz
  * r/Shaneee92
* AMD-OSX
  * QuickTime
  * fozteh
  * Brass Ensemble
  * Villegasdv
* Other
  * Every link within [Resources](#resources), without your tools and guides this would not be possible!

## My Build Components

| Component     | Type                             |
|---------------|----------------------------------|
| SMBIOS Model | iMacPro1,1                        |
| Motherboard  | ASUS TUF X570 Plus                |
| CPU          | AMD Ryzen 3700X                   |
| GPU          | Sapphire Nitro+ 5700XT            |
| RAM          | 2x16gb Ballistix Sport AT 3200Mhz |
| WiFi / BT    | N/A                               |
| Ethernet     | Realtek® L8200A                   |


## Getting Started

1. Read the guides listed within [Resources](#resources) so you can grasp an understanding of what is going to be happenning.
2. Download GibMacOS, OpenCore, and YOUR necessary KEXTs.
3. Make sure you have a flashdrive of at least 16gb that has been formatted to NTFS.
    * Right click on the flashdrive within the file explorer.
    * Select format
    * Change the format type to NTFS.
    * Select Quick Format.
4. Read and follow the steps listed below carefully. If you have questions you can contact me on reddit r/xJetSetLifex or on the AMD OSX Forums - xJetSetLifex

## Downloading Catalina

1. Run gibMacOS.bat as an Administrator.
    * Upon first opening it, it will downlaod some required files. There is nothing to be worried about.
    * If it asks you to install any missing files / programs, press y and ENTER (for yes).
2. Select the version you want to download.
    * The most current version at the time of writing this is Catalina 10.15.2.
    * You can enter R as you only technically need the recovery.dmg and this will save you some time, however I would recommend to play it safe and download the whole update.
3. Select the number that represents the udate you want to download and press ENTER.
4. Give it some time to download all of the necessary files and once finished press ENTER to return to the main menu.
5. Then type Q and ENTER to close the command prompt.

## Creating the USB

1. Run MakeInstall.bat as an Administrator.
2. View the drives listed within the command prompt and select the number that correspeonds to your flashdrive. Then press ENTER.
    * IT IS CRUCIAL YOU SELECT THE CORRECT DRIVE AS ALL DATA WILL BE REMOVED!
3. Press y and ENTER to confirm your selection.
4. Within the gibMacOS folder navigate to macOS Downloads/publicrelease/*Version You Downloaded*.
5. Hold Shift and right click on RecoveryHDMetaDMG.pkg and choose Copy as Path.
6. Navigate back to the command prompt and right click where the blinking cursor is displayed.
    * It should paste the path you just copied within quotation marks.
7. Press ENTER and be patient! It will begin to extract the files necessary and create a bootable flashdrive.
8. Once finished press ENTER to return to the main menu and then type Q and ENTER to close the command prompt.

## Installing OpenCore

1. Open your USB within the File Explorer and double click on the EFI folder.
2. Select both folders and delete them.
    * gibMacOS installs Clover by default. We are going to be using OpenCore 5.3
    * The name of the flashdrive does NOT matter. It will say CLOVER and that is OK!
3. Open OpenCore-0.5.3-RELEASE.zip and double click on the EFI folder.
4. Select both the BOOT and OC folders and copy them into your flashdrive.
    * When you open your flashrive you should see EFI\BOOT and EFI\OC
    * The main things you are looking for are EFI\BOOT\BOOTx64.efi and EFI\OC\OpenCore.efi

## Adding Kexts, Drivers, and ACPIs

1. Visit the KEXTs link within [Resources](#resources) and download your necessary KEXTs.
    * I recommend only adding what you need! Too many KEXTs can cause panics upon installation, crashes, and failures.
    * KEXTs can be added later once booted into MacOS, as described later.
2. Navigate to EFI\OC\Kexts and and copy over YOUR required .kext folders.
    * You are not moving the files within the .kext folder, you are moving the entire .kext folder!
    * Make sure you have the CORRECT KEXTs for YOUR system! (I had a total of 16).
    * There is tons of information within the [Resources](#resources) listed that goes into detail about what each KEXT is and what it does. There also may be some KEXTs you need that are not listed!
3. The Drivers and ACPIs can be harder to find so if you are looking for the ones I used they will be within the EFI folder linked with this page.
    * The OpenCore Docs go into great detail about what the ACPIs are and what you need to do to get them working!

## Configuring Plist

* Everyone's config.plist may be different as most systems are different!
* The config.plist I used for my system will be linked with this page, so if you have the same system as me feel free to download it.
* Within the config.plist is where you will find manual entries for KEXTs, patches for processors, boot arguments, serial numbers, etc...
* If you add or remove a KEXT you WILL HAVE to edit your config.plist as it may cause panics and crashes at installation.
* Depending on what graphics card you have, you will have different boot arguments.
  * I have a 5700 XT and had to use the following arguments, "-v npci=0x2000 debug=0x100 keepsyms=1 agdpmod=pikera"
  * If you have a 5700 your arguments may look something like this, "darkwake=2 debug=0x100 keepsyms=1 npci=0x2000 shikigva=16 alcid=2"
  * Do your research, read the guides and docs to figure out what boot arguments work best for your system AND your monitor!
* You will notice the serial number and UUID as "X"s at the moment, those will be changed within the SMBIOS section coming up.
* Following the serial number and UUID section of the config.plist is where you will find drivers.
  * If you add or remove drivers you will have to edit this section to avoid panics and crashes at installation.
* Patch locations vary so make sure you read the documentation associated with your processor family that algrey has listed on gitHub!
* This process will require the most trial and error, so don't give up! If you are still struggling to get it working either contact me or head over the AMD-OSX Forum and ask questions!

## First Boot

## Formatting SSD

## Finish Installation

## Adding Clover to the SSD

## Generating the SMBIOS

## Setting up Apple Accounts

## Benchmarks

## Footnotes

