---
layout: article
title: Install and Configure RetroPie
categories: [article, retropie, raspberr_pi]
project: retropie
---

## These are the steps I used to set this up

1. Burn an image of RetroPie to a MicroSD card

   I downloaded the current image of RetroPie (from [here][RetroPie Download]) and burned the extracted image to an SD card. Originally this was retropie-v3.6-rpi2.img, but more recently (when I re-pulled to create a dev SD card for coding) it was retropie-v4.2-rpi3.img. 
   
   I used [IZAc] to extract the compressed image file, and [Win32 Disk Imager] to burn the image to the SD card from my 64 bit Windows 10 laptop. I used a large (128GB) SD card as I had quite a few ROMs.
   
   Then I inserted the formatted SD card into the Raspberry Pi and verified it was functional.
   
   1. OS came up, "resizing primary file group(?)", then rebooted.
   
   2. Came up again. "Welcome no games detected. Hold a button on your device to configure it. Press F4 to quite at any time"
      
      Configuring the keyboard was straight forward. D-Pad was obvious. I used Enter for Start, Space for Seelct, A for A, W for B, S for X, E for Y. I held the space to not add anything for several of the other keys.
      
    3. After configuring the keyboard, I went in to RetroPie config, using the "A" button, and select "WiFi". I then noted my IP Address, so that I could remotely connect and configure the raspberry pi.
    
2. Copy ROMS over to the Raspberry Pi

   I created a "retropie" folder in the root of a thumb drive. Then I inserted the thumb drive into the running Raspberry Pi with RetroPie installed. RetroPie automatically copies over certain "transfer" and configuration directories to the thumb drive.
   
   * BIOS
   * configs
     * from_retropie
     * to_retropie
   * roms
     * atari2600
     * megadrive (Sega Genesis)
     * nes
     * psx (Playstation One)
     * snes   
   
   The LED on the Raspberry Pi blinks to show activity, so I waited until the LED was no longer blinking before removing the thumb drive.
   
   The roms directory contained several default folders. The ones I was concerned with match my game systems. Due to the number of roms, I created sub directories as I felt I needed. I then copied the roms to those folders, moved back to the Raspberry PI, waited for the light to finish blinking, and repeated until all of my roms were copied over. (Because I had a lot of ROMs, and my thumb drive was nowhere near as large as the SD card, I had to repeat this process several times.)
   
   Once the roms were copied over, I restarted the system to make sure they were loaded into the emulation station.    

3. Clean up the list of systems

   I then edited the EmulationStation systems config file (etc/emulationstation/es_systems.cfg) and commented out all systems that I did not want. I found this easier than worrying about where there was and was not folders. Note that in more recent images, the extra systems were not pre-populated, so this was not necessary. 
   
   For the PlayStation (psx) games, some had multiple files. I needed to comment out all the unwanted extensions, leaving only the .CUE files. This only works if you disable the folder search for the system (<https://github.com/Aloshi/EmulationStation/issues/314>). Again, this may have only been necessary in the older versions, as when I attempted to replicate my configuration into a clean system (to take these notes) this was not necessary.
   
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

   ### Scraping
   
   There is a really nice feature in RetroPie where you can "scrape" metadata about the roms. It took a while to go through all of my games, including several restarts, but eventually I exhausted what they were able to find. After scraping, I liked the way it look; however, there were several games that could not be found. I tried adding the data in this screen, but this was combersome. 
   
   So instead of adding the metadata through the scrape screen, I decide to research each game, download my own images, and enter the information directly (in the xml file behind this screen). I copied the downloaded images into system specific subfolders under \configs\all\emulationstation\downloaded_images, then I endterd the information I uncovered about the games into a spreadsheet. I took a look at the system specficic gamelist.xml file for the output structure (from the sub folder corresponding to the system in configs\all\emulationstation\gamelists), and created xml blocks from the spreadsheet using a basic formula. Then I copied the resulting xml to the correct files and verified.

   ### Custom Sub-Folders
   
   I had a ton of games... too many to really find anything. So, I decided to create genre-specific sub folders to store within each system and organize my games. I created sub folders in the ??? directories, then modified the gamelist.xml files (using the same spreadsheet mentioned above) to correctly point to these new directories. I also added images and descriptions of each folder to make navigation easier.
   
   ### Themes
   I didn't like the default theme, so I looked at other themes.
   RetroPie
   ES Themes
   
   I then installed every theme, in order to test them out (on my dev box)
   
   * Tried, but didn't like: Carbon-Centered, Color-Pi, Eudora-BigShot, Eudora-Concise, Flat, Flat-Dark, IO, Material, MiniLumi, Retroplay-Clean-Canela, Retroplay-Clean-Detail-Canela, SimpleBigArt, Simple-TurtlePi, Simplified-Static-Cenela, Space , Turtle-Pi, Workbench
   
   * Possible Options: Carbon, Clean-Look, Eudora, Fundamental, Luminous, MetaPixel, NBBA, Pixel, Pixel-Metadata, Pixel-TFT, Simple, Simple-Dark, Spare, TronkyFran, Zoid
   
   I ended up picking TronkyFran. I like the simple game page, with all of the details, as well as the background images on the games. I uninstalled all themes that I didn't like. 
   
   ### Splash Screen
   
   I am not sure if I want a custom splash screen or not. To start out, I wanted to take a look at what they had. <https://github.com/RetroPie/RetroPie-Setup/wiki/Splashscreen>
   
6. Update RetroPie - <https://github.com/retropie/retropie-setup/wiki/updating-retropie>

7. Backup entire RetroPie SD card to an image file.

   I had actually backed up the SD card along the way, sometimes copying only the config file, and other times "burning" a new .IMG file (using Win32DiskImager). After I had finished making changes and felt I understood the system enough to rebuild it from scratch, I paired it down to only a few key folders.

## Rotate Pi
* ds

## Other things to play with:

* Test experimental child-safe mode

* Find ideal theme, including downloading them

* Hide extra startup text

* Add script to write out which system is active (RetroPie, Config, or an Emulator... and which one)

   <http://www.circuitbasics.com/how-to-write-and-run-a-shell-script-on-the-raspberry-pi/>
   <https://www.raspberrypi.org/forums/viewtopic.php?f=27&t=13475>
   <https://github.com/RetroPie/RetroPie-Setup/wiki/runcommand>

* "Changing Disc" in multi-disc rom: <https://github.com/RetroPie/RetroPie-Setup/issues/233>

* Cross-System folders to chronical the evolution of specific series or genres. <https://retropie.org.uk/docs/Add-a-New-System-in-EmulationStation/>

* Add game search

[RetroPie Download]: https://retropie.org.uk/download/
[IZAc]: http://www.izarc.org/
[Win32 Disk Imager]: https://sourceforge.net/projects/win32diskimager/
[RetroArch]: http://www.retroarch.com/
