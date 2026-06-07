---
layout: post
title: Me and my Logitech MediaPlay mousie and Linux
date: 2005-01-07 23:31:59.000000000 -08:00
published: true
categories:
- Life in General
tags: []
permalink: "/2005/01/07/me-and-my-logitech-mediaplay-mousie-and-linux/"
---

One word seems to fit... WAHOO!!! A couple of weeks ago, I bought [this incredibly cool Logitech MediaPlay mousie](http://www.logitech.com/index.cfm/products/details/US/EN,CRID=2135,CONTENTID=9340). Now, I run Linux by choice, and have for the last 10 years, and most probably will for the next 20 or so. This means that there are certain things you resign yourself to having to figure out yourself.

This mousie was one of them. I mean, the smooth scrolling, and etcetera worked fine, as did the 3 other buttons (X sees 5 buttons for a normal 3 button mouse with a scroll-wheel--3 regular and buttons 4 and 5 are the scroll-wheel's up and down). So, that much worked fine out of the box. But this cute little mousie has 10 other buttons!! It has side-to-side scroll, universal back/next, media launcher, media play/pause, media volume up/down, and media back/next. 15 buttons altogether!! =:) And after a bit of work, they all work PERFECTLY from within Linux!! From [the reviews I've read about this mousie on Amazon](http://www.amazon.com/exec/obidos/tg/detail/-/B0002SAF3C/qid=1105157980/sr=8-1/ref=sr_8_xs_ap_i1_xgl23/103-4088914-6664637?v=glance&s=electronics&n=507846), that's saying more than what people are saying about this mouse in that other popular operating system. But anyway, I digress...

First, it's possible to do no complex hackery at all and get buttons 6 and 7 working. Firefox and Opera both understand these buttons as back and next, so by just doing this to your XF86Config (or xorg.conf):

> Section "InputDevice" Identifier "Mouse0" Driver "mouse" #Option "Protocol" "IMPS/2" Option "Protocol" "ExplorerPS/2" Option "Device" "/dev/input/mice" #Option "ZAxisMapping" "4 5" Option "ZAxisMapping" "6 7" Option "ButtonNumber" "7" Option "Buttons" "7" EndSection

... and this on your command line:

> xmodmap -e "pointer = 1 2 3 6 7 4 5"

... you can have that working. But that wasn't enough for me, and it shouldn't be for you either. =:)

Enter [this sweet little project](http://freshmeat.net/projects/lmpcm_usb/) by David Oliveira. I have posted on that page in great detail all that I've done to get things working perfectly for me, so I'll leave it up to the reader to follow that far for the detailed directions. It's quite easy, though, thanks to the work that David has done on the kernel module.

Anyway, again, WAHOO!!! My cute little mousie is now fully integrated into KDE. The media button launches [amarok (which fully rocks in stereo)](http://amarok.kde.org/), volume up and volume down do just that, and KDE displays a nice OSD showing what it's doing. I have the play/pause and media next/previous buttons controlling amarok's playlists.

This is by far the best "fuzzy" feeling that I've had in Linux in a while, and it feels quite good and satisfying, I must say. =:)

Long live the revolution. =;)
