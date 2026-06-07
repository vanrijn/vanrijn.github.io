---
layout: post
title: The Sorry State of VPN'ing in Linux
date: 2007-02-14 16:59:11.000000000 -08:00
published: true
categories:
- Life in General
tags: []
permalink: "/2007/02/14/the-sorry-state-of-vpning-in-linux/"
---

Just a warning, this is a bloody rant:

Novell's Nortel VPN package comes REALLY close, but it doesn't handle PIN/RSA SecurID yet. PLEASE get this working guys!! In fact, please hire me and pay me to get it working!!! =;) The ONLY choice you have in Linux (if you find yourself needing to connect to a Nortel VPN that uses SecurID) is to fork over $100 for Apani's Contivity client for Linux. Oh--and, by the way, you can't use that on SUSE 10 or any other modern distribution, since it's still looking for gcc3 and other things that aren't found on my SUSE 10 laptop. Although, to be fair, the Apani support guys are very quick in their e-mail replies and I've learned that they're working on an new client by end of first-quarter, which will be welcome. But we really need a completely free VPN solution for Linux that interfaces with Nortel's VPN!!!

Also, VMWare 5.5 finally allows you to use a bridged wireless network connection! Unfortunately, if you use madwifi wireless drivers, as I do, you'll get errors like this:

> bridge-ath0: enabling the bridge bridge-ath0: can't bridge with ath0, bad header length 88 bridge-ath0: interface ath0 is not a valid Ethernet interface bridge-ath0: can't bridge with ath0, bad header length 88

...until you patch madwifi [with this](http://ubuntuforums.org/showthread.php?t=285846). *sigh* More wasted time.

Lastly, I can't tell you how much I hate Windows. I spent far too much time to admit to today trying to connect to my work's VPN in a WinXP VMWare guest from within my openSUSE 10.2 Linux host and kept getting "checking for banner text" timeouts (i.e. the handshake and VPN gets completely established and then the first time data is asked for, it hangs). And then I remembered that I have to disable Symantec's Client Firewall or else it eats these packets. Bloody hell!! The least it could do is tell me it's eating them!!!

*frustrated and still sick*
