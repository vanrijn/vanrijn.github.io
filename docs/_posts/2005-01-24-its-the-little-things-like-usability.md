---
layout: post
title: It's the little things, like usability
date: 2005-01-24 23:10:27.000000000 -08:00
published: true
categories:
- Life in General
tags: []
permalink: "/2005/01/24/its-the-little-things-like-usability/"
---

I've been banging my head against the wall for a good couple of hours and had to vent....

I needed to get [Kopete](http://web.archive.org/web/20191019214457/http://kopete.kde.org/) (a REALLY good KDE IM client) to use my Squid proxy server. Well, it's not designed to do that, so that's one thing, but what it can do is use a SOCKS proxy server. I proceeded to set up [the Dante SOCKS proxy server](http://www.inet.no/dante/) on my aging-but-still-ticking debian box. All that's left is getting Kopete to use it, right? Nope, not so easy. You can't have just Kopete use a SOCKS proxy server, like gaim can. You have to have the entire desktop environment (all of KDE) use the SOCKS server. Okay, fair enough and understandable. Ahhh, but then my question for you, oh fair seeker of truth, knowledge and KDE enlightenment, is how the bloody heck you do that.

There's the Proxy configuration settings dialog in KDE's control center. And it has 2 tabs... Proxy and SOCKS. One would think that one could just go to the SOCKS tab and enable SOCKS support, right? Well, at least for me (running Fedora Core 3), this doesn't work. Every time I tried to enable Dante support, I got an error saying "SOCKS could not be loaded" or some-such. I had to download [dag's dante RPM](http://dag.wieers.com/packages/dante/) to get the libsocks library, and then set this up as a custom library. This was a pain, but after that, things should just work swimmingly, right? Wrong.

KDE uses a combination of the 2 tabs--Proxy AND SOCKS. You have to change the Proxy settings from "direct connection to the internet" to something other than that. And, again, my question for you, oh fair seeker of truth, etc., is what you are supposed to use??? Unlike with firefox, where you can specify the SOCKS server easily (there's a text field that says "SOCKS server:"), there is no place to do this in the Proxy dialogs. The ONLY way I could figure out how to get this bloody thing working is to write my own simple auto-proxy-configuration file and have KDE use that.

The REALLY annoying thing to me about all of this is that I could not find ANY documentation on the 'net or the KDE site on how to do this!!! Surely there must be a simpler, more correct way. I'm putting my money on my KDE RPMs being screwed up, or possibly in me missing an RPM or something. *sigh* But MAN, this was annoying.

Having said all that, however.... The coolest little bit of magic that I learned tonight was the [brilliance that Netscape created more than 8 years ago](http://web.archive.org/web/20210311092430/http://wp.netscape.com/eng/mozilla/2.0/relnotes/demo/proxy-live.html). Think about that! 8 years ago. =:) Anyway, said brilliance is an auto-proxy configuration standard that Netscape created that lets you tell the browser what proxy settings to use, and it can be as complex as desired. For the time being, I want all web queries to go to my SOCKS proxy, so my file looks something like this:

> function FindProxyForURL(url, host) { return "SOCKS localhost:1080"; }

Literally--that's it. Just put that into a text file and save it as is. I'll likely expand it later to be more complex, but for now, it does what I want it to.

Okay, I feel better now.
