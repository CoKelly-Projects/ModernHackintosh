# Modern Hackintosh Guide

## DISCLAIMER

This is a guide for Windows 10 based systems. I am not responsible for any damage caused to your components, data loss, or anything else that may happen throughout this process. Follow this guide at your own risk! The steps listed below worked for my components. You will find my components listed under the [My Build Components](#my-build-components) section. There is no guarantee this guide will work for your components. You are responsible for reading about and knowing the guides, documentation, and programs listed below. You may need to download additional programs and seek other resources than what is listed. The steps within this guide are for AMD based components, however there are links within [Resources](#resources) that have steps for Intel and NVIDIA based components. Without further ado, good luck and ask questions!

## Table of Contents

1. [Resources](#resources)
2. [Credit](#credit)
3. [Build Components](#my-build-components)
4. [Getting Started](#getting-started)
5. [Downloading Catalina](#downloading-catalina)
6. [Creating the USB](#creating-the-usb)
7. [Installing OpenCore](#installing-opencore)
8. [Adding KEXTs, Drivers, and ACPIs](#adding-kexts-drivers-and-acpis)
9. [Configuring config.plist](#configuring-plist)
10. [First Boot](#first-boot)
11. [Formatting The Main Drive](#formatting-the-main-drive)
12. [Finishing the Installation](#finish-installation)
13. [Adding Clover to the Main Drive](#adding-clover-to-the-main-drive)
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
  * r/johnklos
* AMD-OSX Forum
  * QuickTime
  * fozteh
  * Brass Ensemble
  * Villegasdv
  * pulsar7377
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

1. Read the guides listed within [Resources](#resources) so you can grasp an understanding of what is going to be happening.
2. Download gibMacOS, OpenCore, and YOUR necessary KEXTs.
3. Make sure you have a flash drive of at least 16gb that has been formatted to NTFS.
    * Right click on the flash drive within the file explorer.
    * Select format
    * Change the format type to NTFS.
    * Select Quick Format.
4. Read and follow the steps listed below carefully. If you have questions you can contact me on reddit r/xJetSetLifex or on the AMD OSX Forums - xJetSetLifex

## Downloading Catalina

1. Run "gibMacOS.bat" as an Administrator.
    * Upon first opening it, it will download some required files. There is nothing to be worried about.
    * If it asks you to install any missing files / programs, press "y" and "ENTER" (for yes).
2. Select the version you want to download.
    * The most current version at the time of writing this is Catalina 10.15.2.
    * You can enter "R" as you only technically need the "recovery.dmg" and this will save you some time, however I would recommend playing it safe and downloading the whole update.
3. Select the number that represents the update you want to download and press "ENTER".
4. Give it some time to download all of the necessary files and once finished press "ENTER" to return to the main menu.
5. Then type "Q" and "ENTER" to close the command prompt.

## Creating the USB

1. Run "MakeInstall.bat" as an Administrator.
2. View the drives listed within the command prompt and select the number that corresponds to your flash drive. Then press "ENTER".
    * IT IS CRUCIAL YOU SELECT THE CORRECT DRIVE AS ALL DATA WILL BE REMOVED!
3. Press "y" and "ENTER" to confirm your selection.
4. Within the gibMacOS folder navigate to macOS Downloads/publicrelease/*Version You Downloaded*.
5. Hold "Shift" and right click on "RecoveryHDMetaDMG.pkg" and choose Copy as Path.
6. Navigate back to the command prompt and right click where the blinking cursor is displayed.
    * It should paste the path you just copied within quotation marks.
7. Press "ENTER" and be patient! It will begin to extract the files necessary and create a bootable flash drive.
8. Once finished press "ENTER" to return to the main menu and then type "Q" and "ENTER" to close the command prompt.

## Installing OpenCore

1. Open your USB within the File Explorer and double click on the "EFI" folder.
2. Select both folders and delete them.
    * gibMacOS installs Clover by default. We are going to be using OpenCore 5.3
    * The name of the flash drive does NOT matter. It will say CLOVER and that is OK!
3. Open "OpenCore-0.5.3-RELEASE.zip" and double click on the "EFI" folder.
4. Select both the "BOOT" and "OC" folders and copy them into your flash drive.
    * When you open your flash drive you should see EFI\BOOT and EFI\OC
    * The main things you are looking for are EFI\BOOT\BOOTx64.efi and EFI\OC\OpenCore.efi

## Adding Kexts, Drivers, and ACPIs

1. Visit the KEXTs link within [Resources](#resources) and download your necessary KEXTs.
    * I recommend only adding what you need! Too many KEXTs can cause panics upon installation, crashes, and failures.
    * KEXTs can be added later once booted into MacOS.
2. Navigate to EFI\OC\Kexts and copy over YOUR required .kext folders.
    * You are not moving the files within the .kext folder, you are moving the entire .kext folder!
    * Make sure you have the CORRECT KEXTs for YOUR system! (I had a total of 16).
    * There is a ton of information within the [Resources](#resources) listed that goes into detail about what each KEXT is and what it does. There may be some KEXTs you need that are not listed!
3. The Drivers and ACPIs can be harder to find so if you are looking for the ones I used they will be within the "EFI" folder linked with this page.
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
* Patch locations vary so make sure you read the documentation associated with your processor family that algrey has listed on gitHub! (Found within the AMD Vanilla Install Guide)
* This process WILL most likely require some trial and error, so don't give up! If you are still struggling to get it working either contact me or head over the AMD-OSX Forum and ask questions!

## First Boot

* First thing is first! View the OpenCore Guide and change your BIOS to the recommended settings.
  * These are not guaranteed to work and different motherboards may require different settings than what is listed.
* After you change your BIOS settings, save, and restart the system, you will want to open the boot menu.
  * I have an ASUS board and the boot menu is "F8" upon startup.
  * Refer to your manual for your board's boot menu button.
  * You can also change the boot priorities within the BIOS if you cannot find your boot menu button.
* Select the USB flash drive as the designated boot device.
  * It should say "UEFI" and then the name of the flash drive.
  * It is crucial you select "2" and then "ENTER" rather quickly when the options show up. This will select to install MacOS. 
  * Option 1 is to bootcamp Windows. If this gets selected it will create a copy of your Windows drive which may prevent you from getting into your bios. This can be fixed by clearing your CMOS (check your Motherboard manual on how to do so!).
    * This can be avoided by changing "Timeout" value from 5 to 0 from within your config.plist!
* If you have the same components as me and copy my EFI folder, you will see some errors. Disregard as they do not affect the system.
* If you have a different system or require different arguments, drivers, ACPIs, you may come across some errors and will have to do some trouble shooting.
  * Common errors for similar systems include "Prelink Injection... Invalid Parameter", "Kernel Patcher Result... Not found", "AMF: Only X/Y Slides are usable"
   * Prelink Injection: You have to remove the KEXT shown as it is giving errors and preventing it from continuing.
   * Kernel Patcher Result: Do not worry about. You can remove them from the config.plist, but regardless they will not affect the install or performance of the system.
   * AMF: If the system continues to install then do not worry about it. If it shows that and then freezes you may have to mess around with your drivers / boot arguments until you get a working combination. There are tons of resources out there, it jsut depends on your system.
 Assuming you can get everything to install, you will see your screen flood with white text. Leave it alone!
   * There will be a point where it pauses, do not worry! Let it be and it will continue.
   * If you get a black screen after the white text floods then you will have to change your KEXTs and or your boot arguments (most likely boot arguments as this is a graphical issue).
 * After the white text finishes you will get a grey screen and then you will be greeted with the first part of the installation, formatting the SSD.
  

## Formatting the Main Drive

* After the Apple progress bar finishes (GIVE IT TIME!) you will be greeted with MacOS Utilities.
1. Select Disk Utility and CONTINUE.
2. Click the top left "view" button and check "show all devices".
3. Select the partition, HDD, or SSD you want to format for the MacOS.
   * This will be shown as the Manufacturers name of the drive and the size you opted for.
4. Select "Erase" in the top-middle of the window and name the drive whatever you want.
   * Format: MacOS Extended (Journaled)
   * Scheme: GUID Partition Map
   * Click "Erase".
5. Once completed click "Done" and close the disk utility.
   * Do not worry, this is only closing the Disk Utility portion you opened earlier. You will be redirected to the main menu.
6. Select "Reinstall MacOS" and "Continue".
   * Continue, Accept the License Agreement, and Select the Drive you just formatted (It should be the only one available).
7. Click "Continue" and let it do its thing!
   * This process will vary depending on a lot of parameters (it took me about 1 hour).
   * During this time, BE PATIENT, and ensure the screen does not go to sleep. If it does, wake it up ASAP to prevent anything from happening.

## Finish Installation

* When the installation finishes the computer will restart. Do what you did before to get back into the boot menu and select the flash drive once again.
* Select "2" and "ENTER" again to continue with the installation.
* Again, the screen will flood with white text. Once completed it will continue to install the MacOS.
  * This part varies on many different parameters, but it only took me about 5 minutes.
* Once it finishes the computer will restart and again you will need to enter the boot menu and boot from the flashdrive.
* Again select "2" and "ENTER as this will finish the installation.
   * If it gives you an error that says "Boot Failed" then unplug the flash drive, restart the computer, and plug the flash drive back in.
   * If you did not get an error, the screen will flood with white text and once the progress bar finishes you will be greeted with the setup of MacOS!

## Adding Clover to the Main Drive

Congratulations! If you made it this far then you have successfully installed MacOS!
* Go through the set up. I opted out of all informational data and turned everything off I did not want or did not want Apple to find out.
* I added my iCloud account within this step, but if you opt out for now there will be instructions on how to add it later once everything is setup.
1. Open Safari and search for "Clover Configurator".
2. Download it from "Mackie100Projects" and press "Allow" to allow it to download.
3. Open the Clover Application you just downloaded.
   * If it does not allow you to open it or gives you an error go to System Preferences > Security and Privacy > "Open Anyway" (bottom right of the window) > "Open"
4. With Clover opened, select "Mount EFI" on the left-hand side, select your drive (with the name you gave it), and select "Mount Partition".
5. "Open Partition" and open the "CLOVER" disk on the right-hand side of the desktop.
6. Drag and drop the "EFI" folder from the "CLOVER" disk to your drive partition you just opened.
7. Close both windows and select "Unmount Partition" in the Clover Application (grey text above Open Partition).
8. Click the Apple logo on the top left of the screen and select "Shut Down" (this may take a second).
9. Unplug the flash drive and boot into the boot menu once more.
  * You should now see both your Windows Drive and a "UEFI" drive that has the MacOS system on it.
  * Select the MacOS drive, select "2" and then the screen will fill with white text. This will be the normal procedure for booting into MacOS from here on out. The flash drive is no longer needed but recommended to keep in case you run into any problems and need to reinstall MacOS.
  * Enter your password and everything should be just as you left it.

## Generating the SMBIOS

1. Open the Clover Configurator Application and mount your drive once more.
2. Open the partition and navigate to your config.plis file
3. Open the config.plist file and select the "Text Mode" within clover configurator.
   * This should allow you to edit the config.plist
4. Select the "SMBIOS" section within Clover Configurator and select the two directional arrows on the right-hand side by "Check Coverage".
5. Select the best SMBIOS that matches to your hardware (I used iMacPro1,1).
6. Randomize the Serial Number and the UUID a couple of times.
7. Copy and paste your Serial Number and UUID from the SMBIOS section into your config.plist.
   * Use "Ctrl+F" and type "Serial" to find your Serial Number.
   * Replace the "X"s with your generated information.
   * Disregard the "MLB" section.
   * Double check to make sure your Serial Number and UUID match!
   * Once you have changed your Serial Number and UUID select "Synchronize" and "Yes" to save changes.
   * Close the text editor, close the partition and reopen it. Navigate back to your config.plist, reopen it and make sure your Serial Numbers were properly changed and saved.
8. Close the text editor and the partition window, saving any changes made.
9. Select "Unmount Partition" again, close the Clover Application, and restart the system.
10. Boot into your MacOS drive and select the Apple logo in the top left corner of the screen.
11. Select "About This Mac" and make sure your Processor is showing (or similar to one you have), RAM is running at the rated speed, GPU is showing up properly, and the Serial Number is correctly displayed.

## Setting up Apple Accounts

* You can either set up your Apple ID at the initial set up, or you can follow the steps outlined below.
1. Open System Preferences and select Apple ID.
2. Enter your email and password.
3. If you have an iPhone or other device tied to that account you may have to go onto that device and approve the sign in.
   * This usually requires a 6-digit combination
   * Once added you can go back to System Preferences > iCloud and change what you want to sync.
   * I recommend restarting the machine once more and allowing some time for everything to sync.
   * If you have not synced in a while then you may have to manually add some contacts, pictures, etc...

## Benchmarks

* Current Benchmarks at the time are as follows: (Note: these have not been optimized to their fullest potential)
  * Geekbench 5.0.4
    * Single-Core: ~1301
    * Multi-Core Score: ~9081
    * Metal Score: ~37633
  * Geekbench 4.4.2
    * Single-Core: ~5952
    * Multi-Core Score: ~39047
  * Cinebench R20
    * Single Core:~496
    * Multi Core: ~4817
  * NovaBench
    * Novabench Score: ~2550
    * CPU Score: ~1548
    * RAM Score - 32gb 3200Mhz: ~371
    * Disk Score: ~132
    * GPU Score: ~499
  

## Footnotes

* From What I Have Tested:
  * What Works
    * iMessage
    * App Store
    * Ethernet
    * Audio
    * Screen Saver

  * What Does Not Work (Note: My Motherboard does not have WiFi or Bluetooth included, nor do I have a WiFi or Bluetooth card / adapter)
    * Bluetooth
    * WiFi
    
* This is a rough outline of the steps I followed to get my Hackintosh up and running successfully. I have not had it set up for that long, so I apologize if this did not go over some things you were looking for. I know the benchmarks and things I have tested are not that long and in depth and I am planning to keep this updated with more tests and information I find out as I use it. I will also update this with pictures so you can see exactly what it is I am referring to. Please leave your feedback, questions, tips, anything either here or direct message me on reddit or the AMD OSX Forum. Thank you for reading this guide, hopefully I was able to help!   
  

