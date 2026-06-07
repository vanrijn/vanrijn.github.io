---
layout: post
title: KPilot Fixes and New Years Resolution
date: 2007-12-31 00:43:51.000000000 -08:00
published: true
categories:
- Life in General
tags: []
permalink: "/2007/12/31/kpilot-fixes-and-new-years-resolution/"
---

Haven't been very good at all lately on keeping my blog up to date. *sigh* Well, for that matter, I haven't been very good at all lately on keeping up with much of anything. But I digress... After [a friendly post from Pablo Yepes](http://thread.gmane.org/gmane.comp.kde.users.pim/11896) about some address book goofiness, I removed the ugly kludge that had been in KPilot for quite a while now:

> r754992 | vanrijn | 2007-12-30 21:49:50 -0500 (Sun, 30 Dec 2007) | 10 lines Changed paths: M /branches/KDE/3.5/kdepim/kpilot/ChangeLog M /branches/KDE/3.5/kdepim/kpilot/conduits/abbrowserconduit/abbrowser-conduit.cc M /branches/KDE/3.5/kdepim/kpilot/conduits/abbrowserconduit/kabcRecord.cc M /branches/KDE/3.5/kdepim/kpilot/lib/options.h * Fixing bug reported by Pablo Yepes on kdepim-users mailing list. We did severe goofiness with middle names... The Palm can't handle them, so we blindly tacked firstname + " " + lastname and stuck it into the Palm's firstname field. The problem is that whenever a copy from palm->pc is done, the kludged first name is transferred to kabc ("firstname middle"). And, it's compounded by every change in either direction. It's an ugly hack and I've removed it. The only way to work around it would be to add an additional check for !firstname.endsWith(abEntry.additionalName()), but that's even sillier. Stop the insanity!

I've also forward-ported the fix to trunk (KDE4), so as soon as I can get around to re-enabling the addressbook conduit in trunk, at least this problem won't be there... =;) Speaking of KDE4.... I keep finding myself with zero time to hack on KPilot for KDE4, but if ever I do, I think I need to approach it more different and more betterer than I have in the past. Bertjan has put a lot of work into unit tests for the new base conduit and keyring code, and I absolutely love it. Haven't taken the time to understand it completely, but I LOVE it. I think that the goal going forward should be that everything in KPilot is unit-test-driven. I need to be able to test all code and code changes without having to physically connect a Palm device to test it with. We'll call that a New Year's resolution. Oh, also, rumor on the streets all over Americana is that the [world-famous Adriaan](http://web.archive.org/web/20251013024556/http://people.fruitsalad.org/adridg/) may just possibly be coming to our little [KDE4 launch party](http://www.kde.org/kde-4.0-release-event/) in January! Oh, that would but rock. =:D
