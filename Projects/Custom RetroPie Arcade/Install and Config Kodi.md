---
layout: article
title: Install and Configure Kodi with RetroPie
categories: [article, retropie, kodi]
project: retropie
---

1. Install Kodi from RetroPie

2. Configure Kodi System (instead of as Ports)  (<http://bobbyromeo.com/technology/raspberry-pi/installing-kodi-retropie-mega-super-guide/>)

3. Tweak Kodi

   * Not powering down display (<http://bobbyromeo.com/technology/raspberry-pi/installing-kodi-retropie-mega-super-guide/>)
   
     Create a directory for kodi scripts
     
     `mkdir /home/pi/kodi_scripts`
     
     Create script to turn the screen off
     
     `sudo nano screen_off.sh`
     
     ```
     #!/bin/sh
     tvservice -o
     ```
     
     Create script to turn the screen back on
     
     `sudo nano screen_on.sh`
     
     ```
     #!/bin/sh
    tvservice -p
    killall -9 kodi.bin
     ```
     echo 0 > /sys/class/backlight/rpi_backlight/bl_power
     sudo bash -c 'echo 1 > /sys/class/backlight/rpi_backlight/bl_power'
     install Kodi Callbacks
     
     Add-ons >> Services >> Kod Callbacks
     
     Configure 
     
     Set up "on idle" event
     
     Set up "on Resume After Idle" 
   
   * Returning to RetroPie 
   
   * Keymap Editor? (<https://www.reddit.com/r/raspberry_pi/comments/2w7n0m/found_out_its_become_very_easy_to_launch_kodi/>)
   4:41
   
   * Auto-Start YouTube (<https://kodifiretvstick.com/kodi-auto-start-install/>)
     <http://kodi.wiki/view/Add-on:YouTube>
   
   * Remote Control
   
   * Cast Videos (Karaoke)
     * <https://www.raspberrypi.org/forums/viewtopic.php?f=63&t=157734>
   
   
   * Other Stuff: 
   
     * <http://www.multibootpi.com/info/how-to-add-a-custom-shortcut-in-kodi/>
     
     * <https://github.com/RetroPie/RetroPie-Setup/wiki/KODI/>
     
     * <http://kodi.wiki/view/Add-on:Kodi_Callbacks>
     * <http://www.triplustutorials.be/category/linux/raspberry-pi/retropie/>
     * <https://www.howtogeek.com/261169/how-to-browse-and-play-terabytes-of-retro-games-from-your-couch-with-kodi/>
     * <https://www.raspberrypi.org/forums/viewtopic.php?t=178108&p=1135256>
     * <https://forum.kodi.tv/showthread.php?tid=309313>
     * <http://bobbyromeo.com/technology/raspberry-pi/installing-kodi-retropie-mega-super-guide/>
     * <https://www.reddit.com/r/raspberry_pi/comments/2z5i7d/install_kodi_over_retropie_adding_custom_menu_art/>
     * <http://kodi.wiki/view/Add-on:Keymap_Editor>