---
layout: post
title: Treo 650, VMWare, HotSync Woes
date: 2006-03-22 16:57:06.000000000 -08:00
published: true
categories:
- Life in General
tags: []
permalink: "/2006/03/22/treo-650-vmware-hotsync-woes/"
---

So, after several weeks of beating my head against the wall, I've found this simple fix for syncing my WinXP guest VMWare virtual machine inside my SuSE Linux host. Basically, it looks like because usbfs wasn't being mounted at boot time, VMWare wasn't getting notified of my Treo 650 as it was trying to HotSync. Make this change in /etc/fstab:

> #usbfs /proc/bus/usb usbfs noauto 0 0 usbfs /proc/bus/usb usbfs defaults 0 0

and/or run this manually if you have to:

> sudo mount -t usbfs usbfs /proc/bus/usb

Thanks VERY much to [andyb](http://andyspace.me.uk/taxonomy/term/2 "helpful tidbit from andyb") for this little tidbit!!!

Oh, and in case you're asking, no, I can't seem to sync evolution/gnome-pilot successfully/consistently with my Treo 650 (yes, I've added the correct lines to devices.xml) and Exchange (couldn't sync the calendar?!?!?), and kpilot doesn't sync with evolution (which is the only OSS thing that can sync with Exchange right now). I blame myself partially, since I could very well spend the time to get kpilot syncing with evolution's databases, and could also spend the time to help get kontact working with Exchange. Blah.
