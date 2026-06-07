---
layout: post
title: KPilot progress(!!) and a fatal Plucker error
date: 2007-08-17 11:19:39.000000000 -07:00
published: true
categories:
- KDE
- KPilot
tags: []
permalink: "/2007/08/17/kpilot-progress-and-how-to-get-around-a-fatal-plucker-error/"
---

First, Bertjan is doing a wunderbar job with the keyring conduit in KPilot/trunk! I stayed up a bit last night and hacked for a while. Felt darned good. One annoyance that we've found, though, is that it looks like KWallet::Wallet (the KDE wallet subsystem) assumes that every program that wants to access the Wallet subsystem will have a top-level window. This assumption is not true with KPilot's syncing daemon (kpilotDaemon). So I've sent an e-mail off to kde-core-devel, and hope to hear something back on it soon, but does anyone in lazy-web-ville know what the Correct (TM) way is to work around this?

Secondly, my darling little Treo 650 just this morning decided to start vomiting on my blue suede shoes every time I tried to open a [Plucker](http://www.plkr.org/) document. Mind you, it worked absolutely perfectly fine before today. And I've installed no new software, etc., between when it worked and now. The error I was occasionally getting was this: "DataMgr.c,Line:11231, Index out of range". Helpful, huh? Fortunately, I found [another poor soul who has hit the same problem and found a solution](http://www.mobileread.com/forums/showthread.php?t=10966). So I downloaded an alternate version of ZLib for my Treo (no idea whether it's the same one that comes with Plucker--it's 4 years old), installed it to my Treo and now things seem to work properly again. I'm not sure what the exact problem was, but installing the [zlib ARMlet Port](http://www.copera.com/zlib-armlet/) seems to have fixed some portion of the problem.

PDA's are amazingly cool little things, when they work. When they don't, however, and insist on rebooting themselves without telling you what broke or how to fix it, you quickly start wondering whether they'll flush cleanly down the toilet or not....
