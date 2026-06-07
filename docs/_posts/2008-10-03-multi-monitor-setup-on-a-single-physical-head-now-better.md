---
layout: post
title: Multi-Monitor Setup On A Single Physical Head (Now Better!)
date: 2008-10-03 14:04:29.000000000 -07:00
published: true
categories:
- Desktop
- KDE
- Linux
tags:
- KDE
- Linux
- VMware
- workstation
- X
- xephyr
permalink: "/2008/10/03/multi-monitor-setup-on-a-single-physical-head-now-better/"
---

That's a big title, eh? I [blogged previously](http://movingparts.net/2008/09/25/a-poor-mans-multi-monitor-setup-on-a-single-physical-head/) about setting up a multi-head X environment for development and testing, even though I'm working on a laptop with only one card. My previous attempt used Xdmx and multiple Xephyr displays, and there were some problems with it. Thankfully, Lubos commented about his [nifty little fakexinerama library](http://ktown.kde.org/~seli/fakexinerama/) that achieves the same result only MUCH easier (easierly?) and without any of the problems that I'd seen using Xdmx/Xephyr(1..n). Here, then, is a description of what I've done and the results....

This is a screenshot from within the Xephyr session, showing the 1600x1200 Xephyr display. The cool thing is that using ksnapshot from within the Xephyr session will actually capture the entire display, not just what fits on your host display. This is important for me because my laptop LCD display is only 1680x1050, so I can't actually fit the entire Xephyr display inside my real physical display. Nice to know, definitely, since this means that I can create a monstrous Xephyr display that doesn't fit inside my actual host display and still get full-display snapshots out of it. So what you see here is a KDE3 session spanning all 4 Xinerama heads. Kicker correctly only spans head 1. VMware Workstation is on head 2, in full-screen mode, but only full-screened on the second head. It can span more than 1 head as I'll show further down.

[![screenshot-ws-fullscreen-enabled]({{site.baseurl}}/assets/2008/10/2910277014_2bec572c4f.jpg)]({{site.baseurl}}/assets/2008/10/2910277014_2bec572c4f.jpg "screenshot-ws-fullscreen-enabled by vanRijn")

To achieve this, I downloaded seli's fakexinerama library, compiled it in ~/build/ like this:

> gcc -O2 -Wall Xinerama.c -fPIC -o libXinerama.so.1.0 -shared ln -s libXinerama.so.1.0 libXinerama.so.1 ln -s libXinerama.so.1 libXinerama.so

I then copied the real /usr/lib/libXinerama.so.1.0.0 to /usr/lib/libXinerama.so.1.0.0.real (make sure you backup your library!) and set up an alias in my ~/.profile so that I can easily switch on and off this fake xinerama library. When I start up my real host session, I don't want to be using fakexinerama, but when I launch my Xephyr session for multimon development, I do need it to be there.

> xin () { if [ "$1" = "real" ] then sudo cp /usr/lib/libXinerama.so.1.0.0.real /usr/lib/libXinerama.so.1.0.0 elif [ "$1" = "fake" ] then sudo cp ~/builds/libXinerama.so.1.0 /usr/lib/libXinerama.so.1.0.0 else echo "real or fake?" fi }

Here's the contents of my ~/.fakexinerama config file:

> #Configuration file ~/.fakexinerama # # The format of the file is rather strict. Lines beginning with # are comments. First line is one # number, specifying number of screens. This line must be followed by this number of lines, each # containing four numbers: X Y W H, i.e. screen's X and Y origin, width and height. 4 0 0 800 600 800 0 800 600 0 600 800 600 800 600 800 600

This establishes a 2x2 4-head xinerama configuration. Next up is creating the Xephyr display. From within your regular host session:

> Xephyr :2.0 -ac -br +xinerama -screen 1600x1200 & xterm -display :2&

You should now have a single Xephyr screen that's 1600x1200 pixels with an xterm running inside of it. Now switch focus to the new xterm window and turn on the fakexinerama library and start up a KDE3 session:

> xin fake startkde # (and when you're done with this little environment, make sure you return your system to sanity by running "xin real")

That's about it. Really cool stuff. One last little screenshot... This one shows VMware Workstation spanning multiple heads. This obviously works with real external monitors as well. The way it works is by clicking the little monitor button to the right of the "View" menu. This tells Workstation to cycle through the available display topologies. So, on first press, Workstation spread across all 4 heads (fullscreen multimonitor, largest topology). Second press took on this configuration that I screengrabbed (vertical span). Third press spread Workstation horizontally across the first 2 heads. And then 4th press returned Workstation to just fullscreen on head 2 (where I started it from).

[![screenshot-ws-fullscreen-enabled-multimonvert]({{site.baseurl}}/assets/2008/10/2909429451_bffc5b2349.jpg)]({{site.baseurl}}/assets/2008/10/2909429451_bffc5b2349.jpg "screenshot-ws-fullscreen-enabled-multimonvert by vanRijn")

One last thought on the subject... One of the things I'm hopefully going to be able to work on in the next couple of months is implementing the new [EWMH _NET_WM_FULLSCREEN_MONITORS hint](http://standards.freedesktop.org/wm-spec/wm-spec-latest.html#id2552578) in various X window managers. Currently, Workstation does some internal gyrations to convince window managers to allow our undecorated fullscreen window to maximize over multiple monitors/heads. _NET_WM_FULLSCREEN_MONITORS was the hint that was recently added to the EWMH spec to correctly accomplish this, but as far as I know, it hasn't been added to any window managers yet. I'm excited about getting the chance to get up to speed on some window manager internals again! It's been a while since I've last had the chance to do that (bbkeys/blackbox days of yore!).

Anyway, hope this helps someone else set up a multi-head dev/test environment, should the need arise. =:)
