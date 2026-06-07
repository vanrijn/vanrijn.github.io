---
layout: post
title: After All That, Back to OS X
date: 2006-04-16 22:51:21.000000000 -07:00
published: true
categories:
- Apples
- KDE
- Life in General
- Linux
tags: []
permalink: "/2006/04/16/after-all-that-back-to-os-x/"
---

So I'm a little disgruntled right now. I've rebooted back into OS X and I'll likely stay here for a while. As it turns out, the show-stopper for me to be able to run Linux (which I'd much prefer) on this powerbook is not anything to do with Linux itself, but rather with the commercial/proprietary software that I find myself needing to run. I need to be able to use Moneydance to do my family's financial account management and bill paying. Moneydance runs on Java. Apparently, the only full version of Java for Linux PPC is IBM's JRE. That's right, Sun doesn't provide Linux-PPC users a JRE, how nice of them. And yes, I did spend a couple of hours trying to get cacao, sablevm, and kaffe working with Moneydance and they didn't work at all. IBM's JRE does actually get the program started and working up to a point. It poops all over itself, however, when it tries to download online bank transaction information:

> There was an error communicating with your financial institution. The details of this error are below. A communication or parsing error occurred. This could be the result of a network problem, a proxy error, or misconfigured server. Error Description: java.io.IOException: java.security.NoSuchAlgorithmException: Class com.ibm.jsse2.cc configured for SSLContext not a SSLContext

Oh joy. I've opened a bug report with the Moneydance folks, but have not heard back from them yet.

And, of course, I can't get any of the non-open stuff to work in Linux PPC. This includes Flash, win32 codecs (can't play .mov, .avi, .wma), etc., etc. So, I need to figure out how to either replace Moneydance with something better that will work in Linux PPC (GNUcash maybe??) and live with the stuff that doesn't work, or I need to figure out how to start being able to be productive and code for KDE in OS X.

Crap. Again... what the heck did I do to myself???

**[Update]** Oh, I almost forgot... The other really big reason I had to sound the retreat is that I kept getting kernel panics whenever I'd go to hotsync my Palm device (Treo 650). I've opened a [bug with the ubuntu folks](https://launchpad.net/distros/ubuntu/+source/linux-source-2.6.15/+bug/39518), and haven't heard back on it yet. My guess would be something related to the appletouch driver, since it's a sort-of-usb device thingey, but I've not had time (nor will I most probably) to look into it further. Blech!
