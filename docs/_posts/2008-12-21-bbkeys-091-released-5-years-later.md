---
layout: post
title: bbkeys 0.9.1 released (5 years later...)
date: 2008-12-21 23:31:07.000000000 -08:00
published: true
categories:
- Linux
tags: []
permalink: "/2008/12/21/bbkeys-091-released-5-years-later/"
---

I installed OpenSUSE 11.1 yesterday and there's some... challenges... that have kept me busy for the last 2 days. But I'll cover those in a different post...

Most relevant to the title is this: OpenSUSE 11.1 doesn't come with blackbox or bbkeys, so I set about compiling them myself and hit some problems. Blackbox, of course, compiled and installed just fine from source. Bbkeys (which depends on Blackbox and its libbt.pc) did not fare so well. For starters, there are some includes missing that newer versions of gcc fail on. Luckily, Art Haas and Egon Braun both sent me in a patch (that I regretably have been sitting on for... a long time...) that addresses this. So I submitted it and a patch I found in OpenSUSE's bbtools SRPM that fixes some string checking tonight and released bbkeys 0.9.1, woot. It felt really good... like old times again... putting a release together of bbkeys. 'twas a nice reminiscence, if nothing else.

The funny thing is... it's been SO long since I've had to think about compiling bbkeys myself, much less coding on it, that there were quite a few cobwebs that I had to clear first before I could get things going. Pretty funny. And, thankfully, it's been a REALLY long time since I last dealt with CVS that I fumbled around for a bit with some simple stuff (wha? "cvs update -C" instead of "cvs revert"??). And there is a small problem with blackbox's libbt.pc that I [submitted a patch for tonight](https://sourceforge.net/tracker/?func=detail&atid=428682&aid=2457221&group_id=40696), that kept me from compiling bbkeys, but after that things went smoothly.

But anyway, it felt good putting a release of my own code out there.
