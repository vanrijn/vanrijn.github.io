---
layout: post
title: KPilot 4.2 progress
date: 2009-01-13 11:10:51.000000000 -08:00
published: true
categories:
- KDE
- KPilot
tags:
- KDE
- KPilot
permalink: "/2009/01/13/kpilot-42-progress/"
---

I discovered a nasty little data corruption bug in KPilot last night and have put some fixes in for it just this morning. The good news is that we didn't lose any data. We just gave you a lot more data. =:) So, if you're helping to test KPilot for our KDE 4.2 release looming Any Day Now (TM), please update from svn (*branches/KDE/4.2/kdepim/kpilot*) and test again. There is still one little nasty behavior that I see that I need to find a fix for tonight, though. With our new core conduit design for KDE 4.2, KPilot keeps its Handheld -> PC mappings in its own XML file--one per conduit. This is a Really Good Thing (also TM). However, it seems that we don't do a 100% perfect job just yet in being rigorous about validating this XML mapping file and when it gets messed up, bad things can happen. So, if you're hitting weird problems with KPilot from KDE 4.2, try removing the XML mapping file for that particular conduit in *~/.kde/share/apps/kpilot/conduits/<PalmUserName>/mapping* and re-syncing. That will force KPilot to do a "first sync" and re-create this mapping from both data sources. I'm not saying that's a good answer, and I'm going to look at finding a solution for the real problem tonight, but it may come in handy for someone out there who's seeing weirdness.
