---
layout: post
title: T61, Suspend, and You
date: 2007-10-28 04:25:08.000000000 -07:00
published: true
categories:
- Life in General
tags: []
permalink: "/2007/10/28/t61-suspend-and-you/"
---

So, along with my glowing accolades of a few days ago, I'll offer a little painful reality. The T61, as I said, is a heck of a nice little machine. Fast, smooth, quiet, and the works. However, there are a few things that have proven to be not so nice: most notably that which is absolutely necessary in a laptop: suspend and resume. I've spent far more time than I'd like searching the 'net for hints/suggestions/hints/etc., but I've not quite found any full, working solutions. It would seem that the problem stems from the fact that I'm using nvidia's binary driver (100.14.23)... or at least that's not helping. Also, it would appear that OpenSUSE 10.3, which I'm running on the T61, is using suspend version 0.69.9, which doesn't happen to know what to do with my T61 model (6549CT0). Oh, another little gem: apparently using the nvidia driver also means that you can't adjust the backlight brightness (FN-Home/End) from within X either. Current workaround: switch to VT 1 - 6 and adjust the brightness from there. This is most certainly an nVidia driver problem, since it works just fine with the VESA driver. Well, I would love to have a totally happy story with no such silliness, but such is life and such is choosing to run Linux. =:) [[ **Update:** ]] Well, shimber me timbers! After yet another day of hacking at things, I still can't get suspend to disk to work on this T61, but I can get suspend to ram working (!!!!!) by putting:

> S2RAM_OPTS="-f"

into the on-OpenSUSE-10.3-non-existent file "/etc/pm/config.d/defaults". Yay!! This makes me much happy. Oh--and don't even try using the "nv" driver... you'll lose your screen entirely. =:/ Progress comes in small steps, apparently.
