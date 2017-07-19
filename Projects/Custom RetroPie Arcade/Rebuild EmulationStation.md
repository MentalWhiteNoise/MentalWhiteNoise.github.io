---
layout: page
title: Updating the Code on EmulationStation
categories: [article, retropie, github, raspberry_pi]
date:   2017-07-13 11:15
project: retropie
---

# Rough, unformatted notes

Files in /EmulationStation

cd /EmulationStation
sudo cmake . -DCMAK_CXX_COMPILER=g++-4.7
sudo make install

/usr/local/bin/emulationstation --resolution 1080 1080 --bottom 400

sudo cp /usr/local/bin/emulationstation /usr/bin/emulationstation

sudo nano /etc/profile.d/10-emulationstation.sh
[ "`tty`" =  "/dev/tty1" ] && emulationstation --resolution 1080 1080 --bottom 400

sudo nano /opt/retropie/supplementary/emulationstation/emulationstation.sh

-- TriggerHappy (ref https://www.raspberrypi.org/forums/viewtopic.php?t=53916&p=412570)
Created new file /etc/triggerhappy/triggers.d/audio.conf
KEY_P 	1	/usr/bin/amixer set Master 5%+
KEY_ENTER	1	/usr/bin/amixer set Master 5%
