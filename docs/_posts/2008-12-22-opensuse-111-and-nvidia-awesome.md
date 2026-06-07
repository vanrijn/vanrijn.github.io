---
layout: post
title: OpenSUSE 11.1 and nVidia == AWESOME!!
date: 2008-12-22 21:39:12.000000000 -08:00
published: true
categories:
- KDE
- Linux
tags:
- nvidia
- opensuse
permalink: "/2008/12/22/opensuse-111-and-nvidia-awesome/"
---

Stark contrast to my [last post](http://movingparts.net/2008/12/22/opensuse-111-and-nvidia/), I know, but I felt it was only fair to blog about the wonders of OpenSUSE 11.1, even/especially with my little nVidia chip. First off, I still think there's something wonky going on with X and/or nVidia's driver in taking so long to start that kdm ends up giving up and committing hari kari, but my little workaround in extending ServerAttempts and ServerTimeout in kdmrc seems to be at least good enough to keep me from committing hari kari myself. And quite honestly, that's about as much time as I want to spend on debugging it. =:/

But I updated to the KDE 4.2 beta2 packages again today and am absolutely loving OpenSUSE 11.1. Things are blazingly fast and well-put-together, and best of all, my faith is totally restored in OpenSUSE after I reinstalled from scratch again. So what changed between my last post and now? A few things:

Yesterday when I installed the KDE 4.2 beta2 packages, I also pulled in the unstable Qt45 packages as well. Maybe that caused some harm? *shrug* All I know is today, I didn't do that and I'm not seeing any problems.

I think I was using my old xorg.conf file (that worked perfectly well in OpenSUSE 11.0, mind you) yesterday, which still had a bunch of tweaks that I added over the last year to get nVidia to play nicely with KDE4. Today, I am just using the default xorg.conf, as written by sax2, and things are REALLY fast and stable. And based on a few comments I've seen (hi jospoortvliet!), it's very likely that this is the true cause of my problems from yesterday. Here's what my old Screen stanza looked like. Does anyone know exactly which one of these might be causing nVidia to hurl its little guts out in OpenSUSE 11.1 with xorg 7.4?

> Section "Screen" Identifier "Screen0" Device "Device0" Monitor "Monitor0" DefaultDepth 24 Option "RenderAccel" "True" Option "UseEdidFreqs" "False" Option "TwinView" "1" Option "TwinViewXineramaInfoOrder" "DFP, CRT" Option "AddARGBGLXVisuals" "True" Option "DisableGLXRootClipping" "True" Option "DamageEvents" "True" Option "TripleBuffer" "True" Option "UseEvents" "True" Option "FlatPanelProperties" "DFP: Scaling = Centered; CRT: Scaling = Centered, Dithering = Enabled" Option "OnDemandVBlankInterrupts" "True" Option "PixmapCacheSize" "2000000" Option "AllowSHMPixmaps" "False" Option "BackingStore" "True" Option "metamodes" "CRT: 1680x1050 +0+0, DFP: 1680x1050 +0+0" SubSection "Display" Depth 24 EndSubSection EndSection

So, in addition to things being extremely awesome in general in OpenSUSE 11.1, I am totally thrilled to finally be able to use powerdevil (it is REALLY nice!!!), and really happy to finally have working hotplug/usb-drive mounting working in KDE 4.2!!!! (it failed hard in OpenSUSE 11.0 due to some hal permissions problems that I never figured out), and zypper (package management) seems to be even faster in OpenSUSE 11.1. And these are just a few of the things that I've noticed in the last couple of hours of X not crashing. =;)

And, of course, KDE 4.2 is continuing to to shape up and look, feel, and perform absolutely marvelously, and OpenSUSE 11.1's beta2 packages are a great way of testing it out.

As for me, I'm just thankful to have a functional laptop again and I hope to get some good KPilot testing and bug squashing done during the next few days of Christmas vacation.

Merry <almost> Christmas, all, and to the OpenSUSE 11.1 guys, a huge thanks again for the awesome new distro. You guys just plain rock! =:)
