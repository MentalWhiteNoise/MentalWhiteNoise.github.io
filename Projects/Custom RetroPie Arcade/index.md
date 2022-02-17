---
layout: project
title: Custom RetroPie Arcade
categories: [project, retropie, raspberry_pi]
date:   2017-07-13 11:15
project: retropie
---

# Adventures in Building an Arcade

I knew how to do very little of what I have done to finish this project. Feel free to follow along and see if you can learn through my experience of having to figure it out!
 
## History

So, a while ago I decided to build an arcade cabinet. I have a collection of old console games, and I wanted to be able to display them, as well as play them. This was greatly inspired by wanting to share some of my childhood with my young daughter. 

But, I ran into a problem. In researching, it was gonna be a pain to wire up all of the different controllers to an arcade style control, so that the controller can be switched. So, the project went where many of my projects go... on a shelf. 

## Raspberry Pi & RetroPie

Okay, not to understate it, but ([Raspberry Pi]) a $35 computer designed to hack and try and do cool things with? SOLD! Add to that prebuilt software that you can install to quickly convert that hardware into a console emulator ([RetroPie])? The project is practically done!

[Check out how I installed and configured my Raspberry Pi](Articles/Install and Config RetroPie)

## But what about the monitor?

So, the cabinet itself is easy. I have been an amateur woodworker since ~16. But what do I do about a monitor? Searching around it's easy to find actual arcade monitors... even old school CRT behemoths! But, wow, they're expensive! And I want to use the cabinet as a display for my old console systems and games... a CRT would take up too much space. Modern TVs are cheap, but the aspect ratio on them is all wrong... 16:9 vs 4:3 of the old television sets... and most arcade games were actually 3:4 (taller vertically than horizontally). I know, I can get a modern LED or LCD TV, and simply turn it sideways! No... that'll be too tall. I want the arcade to fit two players side by side...

You see the problem and how a solution unfolded. What I ended up doing is getting a large display model TV (no remote or stand... works for me!) and turning it... but hiding a good chunk of the screen above and below opening in the arcade cabinet (behind the marquee and control panel, respectively). This worked great... except how to I rotate and crop the software?

## Rotating the Software

Well, I did some research! I ended up adjusting the [config file][config.txt] in [Raspbian], as well as the startup of the [EmulationStation]. But, to get the EmulationStation to scale text correctly, and center properly on the cropped screen, I had to dig into the code. 

If you are a programmer, you probably already know all about the awesomeness of [GitHub] and the power of open source. If you are interested at all in programming, I encourage you to take a look! Either way, EmulationStation (and most if not all the other pieces of software used in the RetroPie) is open source ([here][EmulationStation GitHub]). This means it was easy to get the code, and there was even a helpful post on how to make changes! It was still far from easy for someone who is not an experienced programmer to find where things needed to be changed and figure out how to build and deploy those changes... but I was able to!

[Check out how I was able to rebuild the EmulationStation with my changes](Articles/Rebuild EmulationStation)

## Adding "Multiple System" Folders

* <https://retropie.org.uk/docs/Add-a-New-System-in-EmulationStation/>

* Note: had trouble creating the link (ln <https://wiki.debian.org/SymLink>) files. My issue was I was accidently using relative paths, instead of global. Also, I did not link ALL files, only the ones set up in the menu. This cased PlayStation roms (which almost always had multiple roms associate by a cue file) to not work.  

## Karaoke?

* <https://retropie.org.uk/docs/KODI/>

* <http://kodi.wiki/view/Add-on:YouTube>

* <http://bobbyromeo.com/technology/raspberry-pi/installing-kodi-retropie-mega-super-guide/>

## Issues with Sega Genesis only using three buttons

* <https://github.com/retropie/retropie-setup/wiki/Genesis-Megadrive>

## Store ROMs in a thumb drive (?) 

* <http://bobbyromeo.com/technology/raspberry-pi/installing-kodi-retropie-mega-super-guide/>

* Mount and automatically connect a thumb drive
  <https://www.raspberrypi.org/forums/viewtopic.php?f=63&t=38058>
  
  If you  
  ```
  sudo nano /etc/fstab
  ```  
  then add the line to the end
  ```
  /dev/sda2 /mnt/usb vfat defaults 0 2
  ```
  it should mount at boot, assuming the sda2 does not change, which it can if other drives exist at boot up.
  A better option is to use uuid instead of /dev/
  the uuid can be found using the following
  ```
  ls -l /dev/disk/by-uuid/
  ```
  or gparted has the same info
  then your fstab line would start
  ```
  UUID=long_hex_number_from_previous_command /mnt/usb vfat defaults 0 2
  ```
  Using that method means it doesn't matter whether your drive comes up as sda1 or sdb2 or whatever if another drive is in when the Pi is booted.
  I've always used uuid on all of my computers.
  Stu

## Multiboot pi 
* <http://www.multibootpi.com/>
* <https://www.reddit.com/r/RetroPie/comments/5f0xqj/kodi_from_retropie_slow_install_slow_in_general/>

## Rotate & Position Monitor

For touchscreen: <https://www.raspberrypi.org/forums/viewtopic.php?f=108&t=120793>

`sudo nano /boot/config.txt`

```
display_rotate=0 Normal
display_rotate=1 90 degrees
display_rotate=2 180 degrees
NOTE: You can rotate both the image and touch interface 180º by entering lcd_rotate=2 instead
display_rotate=3 270 degrees
display_rotate=0x10000 horizontal flip
display_rotate=0x20000 vertical flip
```
 
## Upcoming steps

Turn off backlight on touchscreen: <https://github.com/Hexxeh/rpi-firmware/issues/96>
 

The arcade has been up and functioning for a while, but there are some things I have yet to finish. 

First, the marquee has not been wired up! I have some ideas about how to make that awesome... but I'll update you with those when I have a chance! Now that my daughter is a little older (8), maybe I'll be able to get her to help me program it. 

Also, right now you need to turn the power for the arcade off completely... there is no safe idle mode. I have a [motion sensor][PIR (motion) sensor] installed right under the marquee, near the upper speakers. Eventually, I have plans to have it use the marquee to draw attention when it is in idle and senses motion, and then come out of idle as soon as any button is pressed. In fact, the reason for me to write up this project now is that I had to go through and review my notes... EmulationStation in the current version has a screen-saver idle mode that I am planning on hooking into, so I had to re-apply my changes (maybe I'll request a pull from my branch?). 

Another issue I should work through, the amp causes the speakers to jump every time it is powered on or off. I plan on getting that resolved... possibly with some simple relays on the speaker wires.

Finally, the cabinet part of the arcade isn't finished! Too many things keep getting in the way... I had a deadline (my brother was coming to visit from France) so I made it functional before I had a chance to finish making it smooth or adding any of the plexiglass for the display section! I need to take it back apart, clean it up, add the plexi and get some decals ordered!  

## Problems

* "Restart System" or "Restart EmulationStation" only exits emulationstation



[Raspberry Pi]:     https://www.raspberrypi.org/
[RetroPie]:         https://retropie.org.uk/
[EmulationStation]: http://emulationstation.org/
[I-Pac 2]:          https://www.ultimarc.com/ipac2.html
[GitHub]:           https://github.com/
[PIR (motion) sensor]: https://www.adafruit.com/product/189?gclid=Cj0KCQjwtJzLBRC7ARIsAGMkOAkFL6ZrbpKmneUBMFTRTypnK4XZHV9Xk23LbmqLy9adR2lH6qxGQAAaAvstEALw_wcB
[config.txt]:       https://www.raspberrypi.org/documentation/configuration/config-txt/
[Raspbian]:         https://www.raspbian.org/
[EmulationStation GitHub]: https://github.com/Aloshi/EmulationStation
