---
layout: post
title: Installing Fedora Linux using a USB thumbdrive
date: 2004-11-09 19:07:15.000000000 -08:00
published: true
categories:
- Life in General
tags: []
permalink: "/2004/11/09/installing-fedora-linux-using-a-usb-thumbdrive/"
---

This is the coolest thing since sliced mustard, just let me tell you!! =:) I spent more time trying to figure out how to do it than actually doing it. As it turns out, Fedora gives you a disk image for precisely this reason.

It turned out like this then....

1) Search Google for a good hour at least, trying to find any references to anyone else doing this. 2) Failing at #1, search for something obscure and find a link to a README for something else which mentions that the diskboot.img is intended to be used for USB thumb drives, etc., and that one should download it instead of boot.iso for this purpose and use dd to get it onto one's USB drive. Note--I cannot find this README now, nor is it in the Fedora/images/ directory where one might think it would be. 3) Download the current [diskboot.img file](http://web.archive.org/web/20080629074251/http://download.fedora.redhat.com:80/pub/fedora/linux/core/3/i386/os/images/diskboot.img) (link for Fedora Core 3--the most current release as of this posting). 4) run "dd if=diskboot.img of=/dev/sda" from a terminal/console.

Then it simply a matter of getting your BIOS to allow you to boot from a USB device. For me and my IBM A31 laptop, I had to enable BIOS USB or some-such, and then move the detected USB drive above my main hard drive in the boot order.

Cool stuff!! Allowed me to pretty painlessly (after I figured out how to do it, exactly) do a network install of the latest Fedora Core release.

One last tidbit... At the boot prompt screen from the diskboot.img, I use "linux xfs askmethod" to be able to install via Network and to be able to use XFS as my filesystem.

Okay, bye.
