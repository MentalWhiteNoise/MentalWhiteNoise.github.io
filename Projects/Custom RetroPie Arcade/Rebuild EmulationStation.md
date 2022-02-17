---
layout: article
title: Updating the Code on EmulationStation
categories: [article, retropie, github, raspberry_pi]
date:   2017-07-13 11:15
project: retropie
---

## Connection

The first step in updating the code
## Rough, unformatted notes

Grant root access for FTP (sftp://retropie):  Set root account Password `sudo passwd root`

Files in /EmulationStation

COMPILE:
cd /EmulationStation
sudo cmake . -DCMAK_CXX_COMPILER=g++-4.7
sudo make install

TEST:
/usr/local/bin/emulationstation --resolution 1080 1080 --bottom 400

PUBLISH:
sudo cp /usr/local/bin/emulationstation /usr/bin/emulationstation

SET SIZE:
sudo nano /opt/retropie/configs/all/autostart.sh
`emulationstation --resolution 1080 1080 --bottom 400 #auto`


sudo nano /etc/profile.d/10-emulationstation.sh
[ "`tty`" =  "/dev/tty1" ] && emulationstation --resolution 1080 1080 --bottom 400
"/opt/retropie/configs/all/autostart.sh"
sudo nano /opt/retropie/supplementary/emulationstation/emulationstation.sh

-- TriggerHappy (ref https://www.raspberrypi.org/forums/viewtopic.php?t=53916&p=412570)
Created new file /etc/triggerhappy/triggers.d/audio.conf
KEY_P 	1	/usr/bin/amixer set Master 5%+
KEY_ENTER	1	/usr/bin/amixer set Master 5%

# Code Changes

1. Screen items resize based on the height of the screen. As it may be shorter from the width, add getScreenSize to get the minimum of the height or the width, and find all uses of getScreenHeight and replace accordingly.

   * Font.h - setting the font size
   * Font.cpp - setting the font size
   * GuiTextEditPopup.cpp - Setting position (DIDN'T CHANGE)
   * GuiMsgBox.cpp - Setting position (DIDN'T CHANGE)
   * GuiInputConfig.cpp - setSize and setPosition (DIDN'T CHANGE) 
   * GuiDetectDevice.cpp - setSize and setPosition (DIDN'T CHANGE) 
   * VideoVlcComponent.cpp - resizeScale (DIDN'T CHANTE)
   * VideoComponent.cpp - scale (DIDN'T CHANGE)
   * OptionListComponent.h - setPosition (DIDN'T CHANGE)
   * MenuComponent.h - TILE_VERT_PADDING (DIDN'T CHANGE... MAY NEED TO!)
   * MenuComponent.cpp - updateSize, maxHeight (DIDN'T CHANGE)
   * ImageComponent.cpp - applyTheme, scale (DIDN'T CHANGE)
   * IList.h - setResize & listRenderTitleOverlay (DIDN'T CHANGE)
   * HelpComponent.cpp - commented out (DIDN'T CHANGE)
   * Window.cpp - init, setResize; renderLoadingScreen, draw, setPosition, and tranlate (DIDN'T CHANGE)
   * Renderer_init_sdlgl.cpp - DECLARE; ADDED getScreenSize!
   * Renderer_draw_gl.cpp - pushClipRect (DIDN'T CHANGE)
   * Renderer.h - added declare for getScreenSize
   * HelpStyle.cpp - position (DIDN'T CHANGE)
   * GuiComponent.cpp - scale (DIDN'T CHANGE)
   
2. I need to be able to adjust the bottom of the screen so it starts part way up the monitor, since part of the TV is behind the controllers. To do this I added a new parameter to the app and wired it up.

   * main.cpp - Added a new optional parameter, --bottom.
   * Renderer.h - Added a new parameter to the init to set the bottom, as well as added the declare for getScreenBottom (optional for later use)  
   * Renderer_draw_gl.cpp - Modified pushClipRect to append the bottom to the initial box.
   * Renderer_init_sdlgl.cpp - 
     * may need to modify SDL_CreateWindow to append the bottom along with the height
     * Added setting the display_bottom during initialization and wired up the glViewport
   * Window.cpp - Added the new bottom parameter to init and wired up passing it to the renderer 
   * Window.h - Added the new bottom parameter to init
    
3. Everything is working good, but I want to be able to scale the default text size...
