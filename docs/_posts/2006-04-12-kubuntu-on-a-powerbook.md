---
layout: post
title: Kubuntu On A Powerbook
date: 2006-04-12 23:48:11.000000000 -07:00
published: true
categories:
- Apples
- KDE
- Linux
tags: []
permalink: "/2006/04/12/kubuntu-on-a-powerbook/"
---

So, in an attempt to get back to hacking/programming again (since I'm definitely not getting it at work), I've installed Linux on my Powerbook. Actually, I'd installed SuSE 10 on it the day after I bought the powerbook 5+ months ago, but I'd never really done anything with it--partly because I really wanted to see what OS X was really like (it is REALLY, REALLY cool, but not conducive to feeling like I can start improving things/hacking/programming) and partly because neither the trackpad nor the wireless ethernet worked. But recently, the folks at the [Broadcom 43xx Linux Driver](http://bcm43xx.berlios.de/) project have made GREAT strides in getting the proprietary Broadcom wireless network card working in Linux. And, the kind folks with the [kubuntu](http://kubuntu.org/)project (probably also the core [ubuntu](http://www.ubuntu.com/) project as well, but I much prefer [KDE](http://www.kde.org)...) have made almost everything work out of the box for Linux running on the Powerbook.

There are a few things that I had to do to get things working as well as I wanted them to. This, then, is some notes on what I've done....

First, the trackpad. By default, the latest kubuntu (Dapper Drake, at time of writing) comes with the driver for the apple trackpad. The kernel module for this is "appletouch." To get it to play nicely with X, I've replaced kubuntu's default section for the Synaptics mouse in /etc/X11/xorg.conf with this:

> Section "InputDevice" Identifier "Synaptics Touchpad" Driver "synaptics" Option "SendCoreEvents" "true" Option "Device" "/dev/input/mice" Option "Protocol" "auto-dev" Option "LeftEdge" "0" Option "RightEdge" "850" Option "TopEdge" "0" Option "BottomEdge" "645" Option "MinSpeed" "0.4" Option "MaxSpeed" "1" Option "AccelFactor" "0.04" Option "FingerLow" "0" Option "FingerHigh" "30" Option "MaxTapMove" "20" Option "MaxTapTime" "100" Option "HorizScrollDelta" "0" Option "VertScrollDelta" "30" Option "SHMConfig" "on" EndSection

And to be honest, after getting used to the Synaptics driver, I really do like the vertical and horizontal scrolling it can do, as well as the right-click and middle-click you can do by tapping with two or three fingers. I do really miss OS X's two-finger scrolling feature, but I think I can get used to this and do just fine. The one thing I still need to spend a little time tweaking is the sensitivity. It seems that I have to tap a little bit harder than I do in OS X to initiate a scroll or a mouse move.

One more mouse-related thing... By default, kubuntu/ubuntu comes with 3 lines in /etc/sysctl.conf that cause the F11 and F12 keys to fire middle/right mouse clicks. I am used to using F11 and F12 for other keybindings, so I've commented these out as such:

> # Emulate the middle mouse button with F11 and the right with F12. #dev/mac_hid/mouse_button_emulation = 1 #dev/mac_hid/mouse_button2_keycode = 87 #dev/mac_hid/mouse_button3_keycode = 88

Secondly, those crazy apple keyboards on the powermacs aren't exactly what you're used to if you've been using x86 Linux for the last 12+ years as I have. It goes "control, alt/option, command (open apple)" on the left side of the space bar. My fingers want to naturally go to the button immediately to the left of the space bar for the "alt" key, and as mentioned, on the apple keyboard, this is the "command" or "open apple" key. So, to map things the way I'm used to working, I have this in a file I've called ~/.xmodmap-powermac:

> keycode 115 = Meta_L keycode 116 = Meta_R clear mod4 clear mod1 add mod1 = Alt_L Meta_L Alt_R Meta_R

I then call "xmodmap ~/.xmodmap-powermac" from either KDE's Autostart directory or ~/.xsession . This causes both the "alt/option" key and the "open apple/command" key to be treated as the "alt" key in X. Happiness.

Now, on to the wireless network... As stated above, kubuntu nicely comes with the kernel drivers for this to work. But there is a little bit of work that is left for the user, because of legal reasons. In short, you need to use the bcm43xx-fwcutter utility from the [broadcom 43xx project page](http://bcm43xx.berlios.de/) to extract the firmware from Apple's drivers. Having done this (read that page for the specifics) copy all resultant bcm43xx*.fw files to /lib/firmware. You'll then need to either reboot (simplest) or reload the bcm43xx kernel module. This will allow the driver to actually use the wireless card.

From there, there's a little bit of a timing issue around getting the card to associate with an AP and subsequently get connected and DHCP'd onto a wireless LAN. But to sum it up, I've added eth0 (the wireless card) to /etc/network/interfaces as so:

> auto eth0 iface eth0 inet dhcp pre-up /home/me/bin/eth0-wireless-pre-up.sh

That tells debian/kubuntu to start the wireless card automatically and how to load it (man interfaces) by running my custom eth0-wireless-pre-up.sh script, which is as follows:

> #!/bin/bash ifconfig eth0 down ifconfig eth0 up iwconfig eth0 channel 6 iwconfig eth0 rate 11M iwconfig eth0 essid MYESSID sleep 2 iwconfig eth0 key MYKEY sleep 2

As you can see, the tricks are that you need to limit the rate for the card to 11M, give it your SID, wait for it to associate to your AP, then give it your key (if you have one), and then after that all works, kubuntu will automatically kick off dhcp (dhclient3, to be precise).

So, that gets my wireless card working at boot. But what about suspending/resuming? Well, there's probably more official ways, but here's what I've done.... I've created a file called /etc/apm/scripts.d/vR-apm and symlinked it into the /etc/apm/resume.d/ and /etc/apm/suspend.d/ directories. That file is as follows:

> #!/bin/sh -x # # apmd proxy script for vR--custom stuffies # -- from apmd_proxy... # Here are the possible arguments: # # start - APM daemon has started # stop - APM daemon is shutting down # suspend critical - APM system indicates critical suspend (++) # suspend system - APM system has requested suspend mode # suspend user - User has requested suspend mode # standby system - APM system has requested standby mode # standby user - User has requested standby mode # resume suspend - System has resumed from suspend mode # resume standby - System has resumed from standby mode # resume critical - System has resumed from critical suspend # change battery - APM system reported low battery # change power - APM system reported AC/battery change # change time - APM system reported time change (*) # change capability - APM system reported config. change (+) # # (*) - APM daemon may be configured to not call these sequences # (+) - Available if APM kernel supports it. # (++) - "suspend critical" is never passed to apmd from the kernel, # so we will never see it here. Scripts that process "resume # critical" events need to take this into account.
>
>
> echo "`date`: got here, 1->$1< -, 2->$2< -" >> /tmp/apm-debug.log
>
>
> case "${1},${2}" in (suspend,*) echo "`date`: doing suspend stuff" >> /tmp/apm-debug.log ifdown eth0 ;; (resume,suspend) echo "`date`: doing resume stuff" >> /tmp/apm-debug.log modprobe -r appletouch modprobe appletouch ifup eth0 ;; esac

And with that, my Linux powerbook correctly restarts the wireless network whenever I suspend and resume (which works perfectly well out of the box too, by the way).

Okay, bye.
