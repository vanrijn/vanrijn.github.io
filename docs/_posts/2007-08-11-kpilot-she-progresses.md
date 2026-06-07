---
layout: post
title: KPilot, She Progresses
date: 2007-08-11 02:33:33.000000000 -07:00
published: true
categories:
- KDE
- KPilot
tags: []
permalink: "/2007/08/11/kpilot-she-progresses/"
---

Woohoo! I ate far too much cheesecake, far too late in the evening tonight, and therefore am still up at 2:30 a.m., hacking on KPilot. And oi(!) does it feel good. =:) We now have a working daemon, a working configuration window, a working kpilot main window, logging happening correctly over the DBus, and with the code that I'm about to commit to trunk, we now are able to get through a hotSync without crashing! W[][]t!

Next on my agenda, if [Adriaan](http://people.fruitsalad.org/adridg/bobulate/) doesn't beat me to it, is to rip every hint out of KPilot's built-in database viewers that makes it look like it could/should/might be able to perform CUD (Creates/Updates/Deletes) actions. Die, devil-bird, die!!

Oh, also, all of the hard work that the talented [Mister Broeksema](http://bertjan.broeksemaatjes.nl/) has been putting into both the base conduit code and the keyring conduit code is really starting to look good. I got this -><- close to being able to sync my test keyring database with the new conduit tonight. I'm sure he'll get it all working proper-like by tomorrow.... =;) In celebration, then, the highlights of my commit comments for tonight:

> - replacing many "emit syncDone(this)" with "delayDone()". I think what might be happening is that syncDone() is deleting our object, which then turns up null in our DEBUGKPILOT stream and blows up (short-lived object maybe too-short-lived?). - adding some safety check in keyringsetup to make sure we have a valid pointer for the wallet. **note** getting a handle on the wallet will block our GUI event thread until it's either successful, or it times out. kinda weird. - _not_ running the installer twice in pilotDaemon. there's no conduit that queues up things to be installed, it doesn't make sense, and it was causing trouble. so out she goes. - replacing "delete thing" with "thing->deleteLater()" in spots for safety's sake - bumping KPILOT_VERSION to pre2 (gonzo). it's the muppets, man, and we have plenty more to go through... plus, it feels like a milestone being that we're actually able to get through a hotsync for the first time in trunk. paaaaaarty time. - woohoo! hotsyncing now works with null conduit. =;)

And now, to sleep, perchance to dream... of getting to do something very much like this for a living... someday....
