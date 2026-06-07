---
layout: post
title: filing cabinet? no. filesystem.
date: 2002-02-24 23:44:52.000000000 -08:00
published: true
categories:
- Life in General
tags: []
permalink: "/2002/02/24/file-systems/"
---

One of the coolest things about Linux is the amazing amount of configurability it offers. One of those things that you're allowed to choose in your Linux machine is the type of filesystem that your Linux machine will use.

Linux has, for the majority of its life, been tied to the ext2 filesystem. That stands for second extended filesystem, not that that means anything to you. But it's a decently-fast filesystem that has done very well for Linux for a long time.

Well, times have changed, etc., etc., and folks are desiring more reliability, fault-tolerance, higher performance, more security, and other valuable features from their filesystems these days. And this is a good thing!

I have poked around a bit amongst these and other mysteries of the universe and have chosen to go with the XFS filesystem for Linux as my first choice. There are others that offer similar benefits to XFS, but for reasons best-described by the authors of XFS (can you say SGI? =:), XFS looks to me to be the next and bestest thing going.

I run debian, as I've said elsewhere, and after researching the subject for a few weeks, I made the decision to go with XFS. Now, this isn't a trivial matter yet, at least not for the debian users, since XFS isn't included in the kernel source that comes from the good Linux kernel maintainers. This will be changing in the near future (yay, yet another soon-to-be-out-of-date page on my site!!!), and XFS will be supported directly by the unpatched kernel, but for the time being, it's a bit above the new-to-Linux crowd in difficulty.

I may come back and describe how I ended up getting a fully XFS-based debian unstable distribution running on my little laptop, but it's not all THAT difficult, and besides, nobody's asked... =:)

But let me just say... XFS has impressed me greatly in the few months that I've been using it--so much so that I've converted my Internet/Intranet development team's main development environment to a fully XFS-based one. =:)

Oh--and remind me to tell you about the joys of getting IBM's Tivoli Storage Manager client (previously ADSM) running on an XFS-based filesystem to play nicely with their server. =:
