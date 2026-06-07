---
layout: post
title: Logitech Marble Mouse and "auto-scrolling" in OS X
date: 2010-08-23 17:12:10.000000000 -07:00
published: true
categories:
- Apples
- Linux
tags:
- Linux
- mac
- mouse
- OSX
permalink: "/2010/08/23/logitech-marble-mouse-and-auto-scrolling-in-os-x/"
---

I love my Logitech Marble Mouse. It's seriously the best mouse I've ever owned. And it works really nicely in Linux, especially thanks to [this excellent Ubuntu wiki page](https://help.ubuntu.com/community/Logitech_Marblemouse_USB). And, reportedly, it works really nicely in Windows too, with Logitech's mouse config software (which does me absolutely no good being that I refuse to run Windows). But I could not get auto-scrolling (where you hold down one of the smaller buttons and move the marble to scroll) to work in OS X.

I almost broke down and bought a new Kensington trackball mouse like the [Kensington K72337US Orbit Trackball with Scroll Ring for PC or Mac](http://www.amazon.com/gp/product/B002OOWB3O?ie=UTF8&tag=movipart-20&linkCode=as2&camp=1789&creative=390957&creativeASIN=B002OOWB3O), [Kensington Expert Mouse Optical USB Trackball for PC or Mac](http://www.amazon.com/gp/product/B00009KH63?ie=UTF8&tag=movipart-20&linkCode=as2&camp=1789&creative=390957&creativeASIN=B00009KH63) (this one still really tempts me), or the [Kensington Slimblade Trackball USB 2.0 for PC and Mac,](http://www.amazon.com/gp/product/B001MTE32Y?ie=UTF8&tag=movipart-20&linkCode=as2&camp=1789&creative=390957&creativeASIN=B001MTE32Y) (this one is sexy as hell!!!), but they each have their flaws. The Orbit is awesome and seems to work in Linux, but it only has 2 buttons. The Expert has 4 totally programmable buttons, and I think it has a physical scroll ring, but I've read that the new model is really bad on your wrist due to the elevated angle. And the Slimblade Trackball looks just amazing, but from what I read, the scrolling is done by twisting the trackball and that's done completely in software, which of course Kensington hasn't provided for Linux.

However, I did find one suggestion that got me to a 95% working solution by reading [Google's cached copy of the second page of this expired Logitech forum post](http://webcache.googleusercontent.com/search?q=cache:DHdZJXfXAAcJ:forums.logitech.com/t5/Mice-With-Mac-READ-ONLY-ARCHIVE/Auto-Scroll-w-Marble-Mouse-in-Mac-OS-X/td-p/102714+auto-scroll-w-marble-mouse-in-mac-os-x/td-p/102714/page/2&cd=1&hl=en&ct=clnk&gl=us). (UGH!) Specifically, Another_User says this:

> I found one that works pretty good using a combination of Smart Scroll and ControllerMate.
>
>
> In controllermate "trackball button 4" box is connected directly to a "toggle" box which is connected to a "button output" box. Properties of the "button output" box are: "when turned on : button down", "when turned off: button up:, "with mouse button: button #7"
>
>
> Smartcontrol actived grabscroll with button#7, check wihtout moving cursors and reversed axis.

So I gave this a shot and got it working! Actually, you don't need ControllerMate. I got this to work by using Logitech's Control Center for OS X, configuring the two small buttons (button 5 and button 4) to report themselves as buttons 7 and 8 by using "Advanced Click", and then I used SmartScroll to pick up on button 7 to do the grabscrolling.

This seems to work really well in OS X applications, like Chrome, etc., but the scrolling doesn't translate well in X apps like NX Client or VNC even. But it's better than it was before, so I'm definitely happier than I was previously.

I'd still love to get the Kensington SlimBlade Trackball working in Linux though. Anyone out there have success getting scrolling with the trackball to work?
