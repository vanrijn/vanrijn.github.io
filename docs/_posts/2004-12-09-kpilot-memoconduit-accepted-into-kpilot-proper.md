---
layout: post
title: kpilot memoconduit accepted into kpilot proper!
date: 2004-12-09 16:13:48.000000000 -08:00
published: true
categories:
- Life in General
tags: []
permalink: "/2004/12/09/kpilot-memoconduit-accepted-into-kpilot-proper/"
---

I realize most won't care about this, but it's an encouragement to me nonetheless. Adriaan has kindly accepted my new memofile conduit into kpilot's CVS repository!! =:) I need to fix it up some as soon as I get a chance and make it [kde-compliant](http://web.archive.org/web/20110513234158/http://developer.kde.org/documentation/library/kdeqt/kde3arch/kde-i18n-howto.html) for translations, etc., and I still need to get my hand-drawn UML diagrams into a tool and into CVS to go with the code, so those are the next 2 things on my todo-list.

Speaking of UML tools....

Umbrello does a very nice job of reverse-engineering my C++ classes, but it does a lousy job with drawing the diagrams. For methods that call other methods internally (you know, like just about every method in the world does???), I can't for the life of me get it to play nice.

Poseidon seems to be a very nice tool.... which can't bring in existing C++ files and in which case is useless to me.

Ditto for Visual UML--and to make matters worse, I think I read that they intentionally pulled out SQD-functionality.

Describe seems to do a semi-decent job of reverse-engineering C++ files, but if it hits something that it doesn't like, it just skips it entirely instead of trying to at least give you something to work with.

Blargh.

Does ANYONE know of a feature-complete (C++ reverse-engineering AND competent drawing functions) UML tool???
