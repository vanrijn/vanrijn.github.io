---
layout: post
title: The Importance of Not Getting Bit While Digging Up Rocks
date: 2006-06-04 01:58:07.000000000 -07:00
published: true
categories:
- Life in General
tags: []
permalink: "/2006/06/04/the-importance-of-not-getting-bit-while-digging-up-rocks/"
---

So, as a prelude... you may think of it as something very important to learn in life... if ever you are planning on digging very, very, very large rocks out of your New England back yard, be sure to cover yourself head to boots in mosquito repellant. Otherwise, you will assuredly find yourself covered in more bug bites than you care to count. I mean, honestly, what kind of stupid mosquito bites you on the ears??? How much blood can possibly be up there anyway? Blah. Death to all mosquitos!!!

Okay, so in other news, I've finally gotten back to coding a bit on kpilot. Feels good. Real good. =:) Granted, all that I've gotten accomplished so far has been getting the thing to compile and install where I want it to, but that includes finally learning a bit of python, discovering and debugging the AAP build system and its recipes, learning more about libtool and -rpath than I'd ever wanted to, and stealing Adriaan's focus for half a day, at least. And none of those are particularly easy things, so I have some sense of accomplishment for this Saturday. =:)

In other, other news, I've finally figured out how to solve the latest 2 anomalies that I've hit with running Linux on my Powerbook. First of all, I learned that I have a "PowerBook5,6" model, as shown by /proc/cpuinfo:

> processor : 0 cpu : 7447A, altivec supported clock : 1499.999000MHz revision : 0.2 (pvr 8003 0102) bogomips : 73.47 timebase : 18432000 platform : PowerMac machine : PowerBook5,6 motherboard : PowerBook5,6 MacRISC3 Power Macintosh detected as : 287 (PowerBook G4 15") pmac flags : 0000001b L2 cache : 512K unified pmac-generation : NewWorld

Secondly, something changed between kernel 2.6.15 and 2.6.17-rc5 that made pbbuttonsd stop working correctly with the function keys (F1/F2/etc.) on my kubuntu ppc system. For some reason, "KBDMode = fkeysfirst " had stopped working. So, I had to pull down the latest source from the pbbuttonsd site and build a .deb out of it. To do this, I did an "apt-get source pbbuttonsd" and copy the contained debian/ directory from it into the new source directory for 0.7.5. I also had to update the debian/changelog entry so that it matched the new version and build time, etc. And then I had to add --without-ibam to the configure flags in debian/rules. Easy enough; had a pbbuttonsd-ppc.deb in several minutes. Installed it, started it, and happily enough, had working function keys again.

I also discovered that building a custom kernel and installing it on kubuntu PPC isn't the same as x86, but it's also not that big of a deal. It's as simple as " sudo make vmlinux modules modules_install" followed by "sudo installkernel 2.6.17-rc5 vmlinux System.map /boot". Granted, you may have to mess with /etc/yaboot.conf and possibly run "sudo ybin -v", but other than that, pretty basic.

Ooh, and the coolest thing is that it's very simple to get your trackpad to ignore any mouse movements or taps while you're typing by doing this: "syndaemon -d -k -i 0.3". I have added this to "~/.kde/Autostart/run-syndaemon.sh" so that KDE will kick it off for me when X starts. And it does require this line in your /etc/X11/xorg.conf: Option "SHMConfig" "on". But other than that, pretty simple.
