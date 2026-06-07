---
layout: post
title: Introducing... a memofile conduit for KPilot
date: 2004-11-17 12:20:51.000000000 -08:00
published: true
categories:
- Life in General
tags: []
permalink: "/2004/11/17/introducing-a-memofile-conduit-for-kpilot/"
---

So, the Knotes conduit in Kpilot doesn't work for me, and several others. After talking with Adriaan de Groot for a while yesterday, I've come to the following conclusions:

1. Knotes is not the right application to be syncing a Palm's memos with.  It doesn't know anything about categories, etc.
2. KJots is close, but that's still not right either.
3. There is no correct memo editor for KDE yet, that is designed to cater to the things that a Palm's MemoDB provides.

So, after discussing these with Adriaan, I'm going to break out my [coding lederhosen](http://dictionary.reference.com/search?r=2&q=lederhosen) and create a Directory/Filesystem-based memofile conduit for KPilot so that I can start syncing my notes again. =:) My goals:

1. Understand enough about KPilot's internals to be dangerous.
2. Understand enough about gnome-pilot-conduits' memofile to be dangerous.
3. Port/recode gnome-pilot-conduits' memofile to a KPilot conduit.
4. Look at the design of the new MemofileConduit after it's working in KPilot and see if redesign/cleanup is needed.

Progress:

- I now have a displaying/functioning-but-not-doing-anything-useful-yet Memofile conduit in my local KPilot code. =:)
