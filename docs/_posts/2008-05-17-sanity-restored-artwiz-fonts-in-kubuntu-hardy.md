---
layout: post
title: 'Sanity Restored: Artwiz Fonts in Kubuntu Hardy'
date: 2008-05-17 02:42:01.000000000 -07:00
published: true
categories:
- Life in General
tags: []
permalink: "/2008/05/17/sanity-restored-artwiz-fonts-in-kubuntu-hardy/"
---

I switched from SUSE 10.3 to Kubuntu 8.04 (Hardy) just this evening. It's always good to get a feel for how the various distros are doing. Anyway, it took me a bit of digging to figure out how to get the artwiz fonts (smoothansi, in particular) to work as my konsole font. Thanks to [this article](http://www.ubuntugeek.com/howto-install-artwiz-fonts-in-ubuntu.html) for the help! Couple of notes: Ubuntu Hardy doesn't ship xfonts-artwiz anymore, apparently. Download them from this [sourceforge project](http://artwizaleczapka.sourceforge.net/). The trick is to tell fontconfig to use bitmapped fonts by running *sudo dpkg-reconfigure fontconfig-config*.
