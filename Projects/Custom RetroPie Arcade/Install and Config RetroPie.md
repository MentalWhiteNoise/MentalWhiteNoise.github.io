---
layout: page
title: Install and Configure RetroPie
categories: [article, retropie, raspberr_pi]
project: retropie
---

## These are the steps I used to set this up

1. Burn an image of RetroPie to a MicroSD card

   I downloaded the current image of RetroPie (from [here][RetroPie Download]) and burned the extracted image to an SD card. Originally this was retropie-v3.6-rpi2.img, but more recently (when I re-pulled to create a dev SD card for coding) it was retropie-v4.2-rpi3.img. 
   
   I used [IZAc] to extract the compressed image file, and [Win32 Disk Imager] to burn the image to the SD card from my 64 bit Windows 10 laptop. I used a large (128GB) SD card as I had quite a few ROMs.
   
   Then I inserted the formatted SD card into the Raspberry Pi and verified it was functional.

2. Copy ROMS over to the Raspberry Pi

   I created a "RetroPie" folder on a thumb drive. Then I inserted the thumb drive into the running Raspberry Pi with RetroPie installed. RetroPie automatically copies over certain "transfer" and configuration directories to the thumb drive. The LED on the Raspberry Pi blinks to show activity, so I waited until the LED was no longer blinking before removing the thumb drive.
   
   I then copied all the ROMs I had (I was able to find and download ROMs for all the games I had on the old systems!) into the "home/pi/RetroPie/roms" folder. 
   
      Here were the folders I copied the ROMs to:
      * atari2600
      * megadrive (Sega Genesis)
      * nes
      * psx (Playstation One)
      * snes  
      
   After the copy finished, I ejected the thumb drive, brought it over to the RPI, and waited for the blinking to stop. Because I had a lot of ROMs, and my thumb drive was nowhere near as large as the SD card, I had to repeat this process several times.

3. Clean up the list of systems

   I then edited the EmulationStation systems config file (etc/emulationstation/es_systems.cfg) and commented out all systems that I did not want. I found this easier than worrying about where there was and was not folders. 
   
   For the PlayStation (psx) games, some had multiple files. I needed to comment out all the unwanted extensions, leaving only the .CUE files. This only works if you disable the folder search for the system (<https://github.com/Aloshi/EmulationStation/issues/314>)
   
   Because I had such a long list of ROMs (particularly for the Atari), I categorized them into genre specific folders. That has made it easier to search through the lists. It also adds to the arcade by letting players find games similar to ones they remember.  

4. Configure controller(s) generally and for each system

   The first time a new controller is connected to RetroPie, [RetroArch] starts up. RetroArch includes a mapping / configuration utility to map functions to specific commands. I took my best guess. 
   
   Then I went through and found images showing the buttons of the various controllers for the consoles I am emulating. I tried a couple of games on a specific emulator, then made note of what I needed to change, both for the first and second person.
   
   Looking through documentation as well as modified dates on various files I was able to track down which files were being updated, and going through the RetroArch config I was able to figure out which buttons were mapped to which keys, and therefore which keys I wanted mapped to which commands for each of the emulators. I ended up manually modifying the config files to get it right, and I believe I still have some issues with some of the mappings (particularly in Sega Genesis). 
   
   Here is a list of the files that I ended up modifying:
   
   * /opt/retropie/configs/all/retroarch.cfg
   * /opt/retropie/configs/atari2600/retroarch.cfg
   * /opt/retropie/configs/megadrive/retroarch.cfg
   * /opt/retropie/configs/nes/retroarch.cfg
   * /opt/retropie/configs/psx/retroarch.cfg
   * /opt/retropie/configs/snes/retroarch.cfg
   
   This link was helpful: <https://github.com/RetroPie/RetroPie-Setup/wiki/RetroArch-Configuration>

5. Configure / pull rom metadata & images

   I wanted my arcade to look cool, so I scraped for images and metadata about the ROMs. For the games I couldn't find, I searched online and pulled images and data manually. This has given my system a cool feel.

6. Update RetroPie - <https://github.com/retropie/retropie-setup/wiki/updating-retropie>

7. Backup entire RetroPie SD card to an image file.

   I had actually backed up the SD card along the way, sometimes copying only the config file, and other times "burning" a new .IMG file (using Win32DiskImager). After I had finished making changes and felt I understood the system enough to rebuild it from scratch, I paired it down to only a few key folders.

## Other things to play with:

* Test experimental child-safe mode

* Find ideal theme, including downloading them

* Hide extra startup text

* Add script to write out which system is active (RetroPie, Config, or an Emulator... and which one)

   <http://www.circuitbasics.com/how-to-write-and-run-a-shell-script-on-the-raspberry-pi/>
   <https://www.raspberrypi.org/forums/viewtopic.php?f=27&t=13475>
   <https://github.com/RetroPie/RetroPie-Setup/wiki/runcommand>

* "Changing Disc" in multi-disc rom: <https://github.com/RetroPie/RetroPie-Setup/issues/233>

[RetroPie Download]: https://retropie.org.uk/download/
[IZAc]: http://www.izarc.org/
[Win32 Disk Imager]: https://sourceforge.net/projects/win32diskimager/
[RetroArch]: http://www.retroarch.com/
