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

## Upcoming steps

The arcade has been up and functioning for a while, but there are some things I have yet to finish. 

First, the marquee has not been wired up! I have some ideas about how to make that awesome... but I'll update you with those when I have a chance! Now that my daughter is a little older (8), maybe I'll be able to get her to help me program it. 

Also, right now you need to turn the power for the arcade off completely... there is no safe idle mode. I have a [motion sensor][PIR (motion) sensor] installed right under the marquee, near the upper speakers. Eventually, I have plans to have it use the marquee to draw attention when it is in idle and senses motion, and then come out of idle as soon as any button is pressed. In fact, the reason for me to write up this project now is that I had to go through and review my notes... EmulationStation in the current version has a screen-saver idle mode that I am planning on hooking into, so I had to re-apply my changes (maybe I'll request a pull from my branch?). 

Another issue I should work through, the amp causes the speakers to jump every time it is powered on or off. I plan on getting that resolved... possibly with some simple relays on the speaker wires.

Finally, the cabinet part of the arcade isn't finished! Too many things keep getting in the way... I had a deadline (my brother was coming to visit from France) so I made it functional before I had a chance to finish making it smooth or adding any of the plexiglass for the display section! I need to take it back apart, clean it up, add the plexi and get some decals ordered!  

[Raspberry Pi]:     https://www.raspberrypi.org/
[RetroPie]:         https://retropie.org.uk/
[EmulationStation]: http://emulationstation.org/
[I-Pac 2]:          https://www.ultimarc.com/ipac2.html
[GitHub]:           https://github.com/
[PIR (motion) sensor]: https://www.adafruit.com/product/189?gclid=Cj0KCQjwtJzLBRC7ARIsAGMkOAkFL6ZrbpKmneUBMFTRTypnK4XZHV9Xk23LbmqLy9adR2lH6qxGQAAaAvstEALw_wcB
[config.txt]:       https://www.raspberrypi.org/documentation/configuration/config-txt/
[Raspbian]:         https://www.raspbian.org/
[EmulationStation GitHub]: https://github.com/Aloshi/EmulationStation
