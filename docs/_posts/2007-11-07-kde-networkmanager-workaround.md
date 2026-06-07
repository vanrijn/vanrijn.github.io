---
layout: post
title: KDE NetworkManager workaround
date: 2007-11-07 15:33:02.000000000 -08:00
published: true
categories:
- KDE
tags: []
permalink: "/2007/11/07/kde-networkmanager-workaround/"
---

In case anyone else hits this.... In one of the more recent releases of our beloved KDE, code was added to more smoothly integrate with networking. Namely, the attempt is now made to be aware of NetworkManager-initiated network connections, as well as know when NetworkManager doesn't think it's connected so as to not keep trying network activities when there might not be a network connection. Excellent idea, honestly. However (you knew there was one), I have a love/hate relationship with NetworkManager and knetworkmanager. When they work, they work great. When they don't it's supremely irritating. Case in point: I'm at a friend's house. He's using standard WEP and a non-broadcasted ESSID. I tried all manners of asking NetworkManager nicely for a good 10 minutes to join the network to no avail. In the next 30 seconds, I manually iwconfig'd, ifconfig'd, and dhclient'd my way onto the network and things are working swimmingly. Almost. You see, with the changes we made (see paragraph #1), now KMail and Konqueror, etc., think that I don't have a network connection because NetworkManager told them I don't. However, I've discovered that I can coax KMail, Konqi, and friends to try using the network connection that I really do have (honestly!) but NetworkManager couldn't provide for me by doing this on the CLI:

> dcop kded networkstatus setNetworkStatus NMNetwork 0

It's hack, but it seems to do the trick for the time being. I'll hunt Will down later and ask him how to do this properly... [UPDATE:] I caught Will and here's the real skinny:

> Either extend your manual connection script to register a fake network with kded that is online, or shoot the networkstatus system down by disabling it in kcmshell kcmkded.  You can also unregister NMNetwork; the system should be fail-safe.  Or not run knetworkmanager.  The system figures the best connection status, so you can also register your own network.  0 is 'no information', 6 is offline, 8 is online in the status enums.

Will rocks, btw. =;)
