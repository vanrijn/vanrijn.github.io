---
layout: post
title: Zypper versus Smart
date: 2008-02-13 02:59:06.000000000 -08:00
published: true
categories:
- Linux
tags: []
permalink: "/2008/02/13/zypper-versus-smart/"
---

sudo zypper update:

> 2 Problems: Problem: No valid solution found with just resolvables of best architecture. Problem: Cannot install java-1_5_0-sun-plugin, because it is conflicting with java-1_6_0-sun-plugin Problem: No valid solution found with just resolvables of best architecture. With this run only resolvables with the best architecture have been regarded. Regarding all possible resolvables takes time, but can come to a valid result. Solution 1: Make a solver run with ALL possibilities. Regarding all resolvables with a compatible architecture. number, (r)etry or (c)ancel> 1 Applying solution 1 Problem: Cannot install java-1_5_0-sun-plugin, because it is conflicting with java-1_6_0-sun-plugin A conflict over java-1.5.0-plugin == 1.5.0_update14 (java-1.5.0-plugin) requires the removal of java-1_5_0-sun-plugin-1.5.0_update14-0.1.i586[opensuse-updates] which is scheduled for installation === java-1_5_0-sun-plugin-1.5.0_update14-0.1.i586[opensuse-updates] === java-1_5_0-sun-plugin-1.5.0_update14-0.1.i586[opensuse-updates] is needed by atom:java-1_5_0-sun-plugin-1.5.0_update14-0.1.i586[opensuse-updates] (java-1_5_0-sun-plugin >= 1.5.0_update14-0.1) findutils-4.2.31-24.i586 is needed by java-1_5_0-sun-plugin-1.5.0_update14-0.1.i586[opensuse-updates] (/usr/bin/find) === java-1_6_0-sun-plugin-1.6.0.u4-0.1.i586[opensuse-updates] === java-1_6_0-sun-plugin-1.6.0.u4-0.1.i586[opensuse-updates] is needed by atom:java-1_6_0-sun-plugin-1.6.0.u4-0.1.i586[opensuse-updates] (java-1_6_0-sun-plugin >= 1.6.0.u4-0.1) Solution 1: do not install java-1_5_0-sun-plugin do not install java-1_5_0-sun-plugin-1.5.0_update14-0.1.i586[opensuse-updates] Solution 2: do not install java-1_6_0-sun-plugin do not install java-1_6_0-sun-plugin-1.6.0.u4-0.1.i586[opensuse-updates] Solution 3: Ignore this conflict of java-1_5_0-sun-plugin number, (r)etry or (c)ancel> ^C

*boggle* sudo smart upgrade:

> Computing transaction...  Upgrading packages (234):   MPlayer                                          kdegames4-carddecks-default   SDL                                              kdegames4-carddecks-other   SDL-devel                                        kdegraphics3-kamera   SDL_image                                        kdegraphics3-pdf   alsa                                             kdegraphics3-postscript   alsa-devel                                       kdegraphics3-scan   alsa-oss                                         kdegraphics4   alsa-plugins                                     kdelibs3   alsa-utils                                       kdelibs3-arts   [snip lots of stuff in between]   kdeedu4                                          qtcurve-kde   kdegames3                                        screenlets   kdegames3-arcade                                 soprano   kdegames3-board                                  transcode   kdegames3-card                                   vorbis-tools   kdegames3-tactic                                 xfsprogs   kdegames4                                        xmoto  Installing packages (4):   kaffeine-lang      kdebase3-runtime   libavahi-qt3-1     libdca0  Removing packages (4):   gnucash         gnucash-lang    ktorrent-lang   slib  571.7MB of package files are needed. 46.3MB will be freed.  Confirm changes? (Y/n): y

Um. Yeah. I think I'll stick with smart for now, guys...
