---
layout: post
title: Thinkpad T61 and Iogear 4-port USB KVM Switch
date: 2007-11-02 13:31:54.000000000 -07:00
published: true
categories:
- Life in General
tags: []
permalink: "/2007/11/02/thinkpad-t61-and-iogear-4-port-usb-kvm-switch/"
---

This, the next exciting story in my Adventures With the Thinkpad T61 At Work (TM) =;).... So I got a really sweet-looking IOGEAR 4-port USB KVM Switch at work. But when I plugged it into the T61, although the nVidia driver was able to find the external display (auto-detect button thingey), it only gave me 2 options for resolution, the larger of which was 640x480, which obviously is rubbish. So I stumbled across this helpful ubuntu page which gave me the clue I needed:

> It would seem that xorg cannot detect the possible resolutions when using the "nvidia" driver. For me, the only resolution I could use was my LCD's native resolution (1680x1050). Here's how you fix this: 1) Make a backup of your /etc/X11/xorg.conf as shown in the previous examples 2) Open /etc/X11/xorg.conf as shown in the previous examples 3) Add the following line to your existing "Screen" section: Option "UseEdidFreqs" "false" If all else fails, try running the following command: sudo nvidia-settings Under Video Configuration set your resolution and refresh rate, click apply, then save X Config.

I added the UseEdidFreqs as false Option, restarted X, and am now happy once again. Hope this helps the next poor soul who hits this... =:)
