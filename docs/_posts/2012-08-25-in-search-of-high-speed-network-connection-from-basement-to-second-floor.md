---
layout: post
title: In Search Of High Speed Network Connection From Basement to Second Floor
date: 2012-08-25 15:50:48.000000000 -07:00
published: true
categories:
- Life in General
- Movies
tags: []
permalink: "/2012/08/25/in-search-of-high-speed-network-connection-from-basement-to-second-floor/"
---

***... or... man, I really don't want to have to run CAT-6 wire from the basement to the second floor....***

So I have a decently-big house. Thank you, God. 2 floors and a finished basement. I have a MacMini server in the second floor bedroom and it's acting as the main audio/video server for the house. I want to have as fast a connection as possible between it and the AppleTV and GoogleTV in the main floor living room. I've already run CAT-6 from the main house router in the basement to the main living room. That was moderately unpainful as we have a drop ceiling in the basement. But there's no easy way to get CAT-6 networking wire run from the basement to the second floor bedroom. I'd have to run wire almost the full length of the house to the conduit I installed last year that runs from the basement to the attic, and then back almost the full length of the house, drill a hole into the bedroom closet wall from the attic, run the wire down it, install a new CAT-6 wall jack, etc. Not the end of the world, but man I'd really like to not have to give up the 8+ hours or so it will take to do it right.

I do have a nice [ASUS RT-N66U Dual-Band Wireless-N900 Gigabit Router](http://www.amazon.com/dp/B006QB1RPY/ref=as_li_ss_til?tag=movipart-20&camp=0&creative=0&linkCode=as4&creativeASIN=B006QB1RPY&adid=0WDTN44D8EQPHF3N3K61) (running DD-WRT) that serves up 802.11 B, G, and N to the house, and the Mac Mini Server is connected right now via 802.11N.

To try to avoid running CAT-6 wire, I figured I'd give the [Netgear XAVB5101 Powerline Nano500 Set](http://www.amazon.com/dp/B007ILFFS6/ref=as_li_ss_til?tag=movipart-20&camp=0&creative=0&linkCode=as4&creativeASIN=B007ILFFS6&adid=17484VJ97T6B63TTNVQE) a try. Got it in from Amazon today (LOVE Amazon Prime!!), and set up a quick test to see how it performs compared to the 802.11 N WiFi connection I already have.

Let's just say that I'm not horribly impressed just yet.

Now, I should state that the EOP (Ethernet over Power) connection/circuit in the basement is on the right side/pole of my house electrical breaker box and the connection/circuit in my bedroom is on the left side/pole. From what I've read, this won't provide the best throughput and that it's better to have both ends of the EOP connection be on the same side/pole. But as a first test, I did file copies over SSH of a 1.5G movie from my MacMini in the second floor bedroom to my MacBook Pro in the basement. I have a solid 1000Mbps connection from the MacBook pro in the basement to the house router. I did 5 iterations of this file copy over the 802.11N WiFi connection and then 5 iterations over the EOP LAN connection, which is advertised as being 500Mbps.

Here's the results I saw over the EOP LAN connection:

# for f in $(seq 1 5); do scp user@MBP:Movies/THE_GREY.m4v THE_GREY-$f.m4v; done THE_GREY.m4v 100% 1471MB 8.6MB/s 02:51 THE_GREY.m4v 100% 1471MB 10.5MB/s 02:20 THE_GREY.m4v 100% 1471MB 10.5MB/s 02:20 THE_GREY.m4v 100% 1471MB 10.5MB/s 02:20 THE_GREY.m4v 100% 1471MB 10.6MB/s 02:19

and here's the results from going over 802.11 N:

# for f in $(seq 11 15); do scp user@MBP:Movies/THE_GREY.m4v THE_GREY-$f.m4v; done THE_GREY.m4v 100% 1471MB 16.2MB/s 01:31 THE_GREY.m4v 100% 1471MB 16.0MB/s 01:32 THE_GREY.m4v 100% 1471MB 16.7MB/s 01:28 THE_GREY.m4v 100% 1471MB 16.7MB/s 01:28 THE_GREY.m4v 100% 1471MB 17.1MB/s 01:26

Wow. That's pretty sad. Roughly 10.14 MB/s on average over EOP LAN and 16.54 MB/s on average over 802.11N. 802.11N, two floors away from the router in the basement, far out-performed the 500Mbps EOP LAN connection. =:( I may move the outlet circuit in the basement so that it's on the same side/pole of the circuit breaker panel to see if that helps the EOP LAN connection, but at this point, I'm not sure I want to spend the time doing so.

Anyone out there travel down this road already? Is it worth it to move the circuit breaker around so that both connections are on the same side/pole? Will that let me get better-than-802.11N speed? Should I be satisfied with the 802.11N connection that seems to be working decently? Is ~ 16MB/s sufficient for 1080p streaming?

Or should I just give up, dedicate a day to the task, and run CAT-6 from the basement to the second floor bedroom?
