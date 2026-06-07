---
layout: post
title: KDE 4.2 (trunk) Now Rocking On My Thinkpad T61!!!
date: 2008-10-03 14:34:10.000000000 -07:00
published: true
categories:
- KDE
- Linux
tags:
- KDE
- kde4
- nvidia
- X
permalink: "/2008/10/03/kde-42-trunk-now-rocking-on-my-thinkpad-t61/"
---

My work laptop and main computing device is a Thinkpad T61 with an nVidia Corporation Quadro NVS 140M (rev a1) card. It's been a frustrating last year in trying to run a KDE4 desktop as my main work and development environment because of the problems with the proprietary nVidia drivers that show up in KDE4. However, this little post is definitely more of a ***Huzzah!!!*** than a disgruntled grousing session. Lord knows we've had plenty of those. =:)

Thanks to the folks at nVidia who are diligently working on improving the problems in their drivers!!

Anyway, I've followed everything I could find on [Lemma's techbase pages](http://techbase.kde.org/User:Lemma/KDE4-NVIDIA) and in the nVidia forums, but nothing has worked. Until now!

I'm running the latest beta from nVidia (177.78). I also discovered that for me, contrary to what everyone else seems to be saying, if I use InitialPixmapPlacement=2, performance is MUCH worse than if I use InitialPixmapPlacement=1. Using the [benchmarking tools](http://techbase.kde.org/User:Lemma/KDE4-NVIDIA#Benchmarking_Changes) from the techbase page, I found that on the [Penrose Tiling test](http://intertwingly.net/stories/2006/07/10/penroseTiling.html), using Opera, the Canvas test would take up to 30 seconds for me if I did "nvidia-settings -a InitialPixmapPlacement=2 -a GlyphCache=1" before running it. However, if I did "nvidia-settings -a InitialPixmapPlacement=1 -a GlyphCache=1" instead, then the Canvas test only took around 2.5 seconds. WOW! So I added "nvidia-settings -a InitialPixmapPlacement=1 -a GlyphCache=1" to my X startup script and was very pleased to discover that KDE 4.2 now is VERY usable on my little laptop!!! Again, ***HUZZAH!!!***

For completeness, then, here is the Screen section from my xorg.conf:

> Section "Screen" Identifier "Screen0" Device "Device0" Monitor "Monitor0" DefaultDepth 24 Option "RenderAccel" "True" #Option "RandRRotation" "True" Option "UseEdidFreqs" "False" #Option "UseInt10Module" "True" Option "TwinView" "1" #Option "TwinViewOrientation" "Clone" Option "TwinViewXineramaInfoOrder" "DFP-0" #Option "UseCompositeWrapper" "True" Option "AddARGBGLXVisuals" "True" Option "DisableGLXRootClipping" "True" Option "DamageEvents" "True" Option "TripleBuffer" "True" Option "UseEvents" "True" #Option "DynamicTwinView" "True" Option "FlatPanelProperties" "DFP: Scaling = Centered; CRT: Scaling = Centered, Dithering = Enabled" Option "OnDemandVBlankInterrupts" "True" Option "PixmapCacheSize" "2000000" Option "AllowSHMPixmaps" "False" Option "BackingStore" "True" #Option "NvAGP" "3" #Option "ConnectedMonitor" "DFP" Option "metamodes" "CRT: 1680x1050 +0+0, DFP: 1680x1050 +0+0"
>
>
> SubSection "Display" Depth 24 EndSubSection EndSection

To be honest, I am not 100% sure which of the recently-changed variables in my setup have resulted in this improving so drastically--whether the new nVidia driver beta (177.78), the xorg.conf changes, or the InitialPixmapPlacement=1 change--but the end result is that I'm now able to use KDE 4.2 (trunk) quite happily and I'm thoroughly stoked about it.

Hope this helps some other poor soul out there. Oh--also, does it sound far-fetched that IPP=1 would work better for me than IPP=2??
