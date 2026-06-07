---
layout: post
title: Bringin' Sexy (urxvt) Back
date: 2008-10-22 12:23:33.000000000 -07:00
published: true
categories:
- Desktop
- KDE
tags:
- Desktop
- kde4
permalink: "/2008/10/22/bringin-sexy-urxvt-back/"
---

Let me tell you a (short) tale, my children. In the dark but awesome olden days, before KDE and GNOME were but glimmers in the eyes of their current communities, there existed a bunch of scrappy hackers who would take the best X applications out there and hack them into submission to their will. Why, I don't have time to tell you of the years where olvwm reigned supreme, nor of the dark days when wm2 brazenly rotated window titles 90 degrees and put window titlebars on the side *gasp!* of the windows, nor of the exciting times when AfterStep was KING, nor the outright courage shown by rasterman who started hacking fvwm2 to do his bidding in exciting and gothic ways. No, sadly, I do not have time to even speak of the days when brave young nyztihke (hi Brad!) started creating his own Blackbox window manager, nor of the intrepid WindowMaker clan (WINGs, anyone?). But back in these ancient days of yore, the killer application wasn't Thunderbird, Firefox, Evolution, nor even xdaliclock. No, my children. The killer application of these dark times was... *pregnant pause* the terminal emulator. (and, incidentally, mutt still kicks butt, but I digress...)

That's right. For back in these dark days, even mentioning that you used a mouse could get you in a whole mess o' trouble. And so this theming thing that you kids *Fluffy Bunny plasma theme? harumph!* take so much for granted now was focused mainly on customizing your X terminal emulator. And I'm not even talking about bash or zsh prompts. I'm talking about cramming your ~/.Xdefaults full of xrdb lines to tweak the snot out of your terminal emulator so that it was the coolest kid on the block. For the simpletons, there was the stodgy old xterm. But soon, along came rxvt, aterm, and the brazen Eterm. We didn't have these fancy tabbed terminal emulators that you kids have now. We had 300 terminal windows stacked carefully and neatly on our 640x480 screens, and we LIKED it! *harumph again*

And so it is with feelings of nostalgia and inner-geekly warmth that I have started using rxvt (urxvt now) again as of late (try as I might, I can't find aterm or Eterm OpenSUSE 11 rpms??). For reasons I will not go into here, having mostly to do with the nVidia card I have on my laptop I'm told, I've been using urxvt for the last week with really good results. It has been a week, almost exactly (`grep Time: /var/log/Xorg.0.log`), since I've restarted X, and I'm not seeing any slowdowns or desktop-switching-slowness. I really like Eterm--especially the font pseudo-shadowing--but I can't seem to get it to do transparency in KDE4. urxvt, however, actually does ARGB visual transparent backgrounds!! `man 7 urxvt` tells the whole tale, but here is my ~/.Xdefaults that I'm quite happy with:

> urxvt.background: rgba:0000/0000/0000/ccdd urxvt.foreground: white !urxvt.font: -artwiz-fkp-medium-r-normal--16-160-75-75-m-80-iso8859-1 !urxvt.boldfont: -artwiz-fkp-medium-r-normal--16-160-75-75-m-80-iso8859-1 urxvt.font: xft:Terminus:pixelsize=14 urxvt.scrollBar_right: 1 urxvt.scrollBar_floating: 1 urxvt.saveLines: 10000 urxvt.internalBorder: 5 urxvt.depth: 32 urxvt.scrollTtyOutput: 0 urxvt.scrollTtyKeypress: 1 urxvt.color12: rgba:6666/6666/ffff/ffff

Anyway, I'm quite happy with how urxvt is looking and acting with this setup in my KDE4 trunk desktop. And besides, there's something about stacking 10 rxvt windows vertically and being able to see the last few lines of output from each simultaneously. =;) Oh, and here's a screenshot showing an urxvt terminal with true ARGB transparent background:

[![screenshot-urxvt-sexiness]({{site.baseurl}}/assets/2008/10/2964672054_64be0c9994.jpg)]({{site.baseurl}}/assets/2008/10/2964672054_64be0c9994.jpg "screenshot-urxvt-sexiness by vanRijn")
