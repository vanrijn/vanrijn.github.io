---
layout: post
title: Changing Background/Wallpaper on OS X With Multiple Spaces and Multiple Monitors
date: 2012-09-25 17:31:02.000000000 -07:00
published: true
categories:
- Apples
- Desktop
tags: []
permalink: "/2012/09/25/changing-backgroundwallpaper-on-os-x-with-multiple-spaces-and-multiple-monitors/"
---

There are a bunch of partial solutions and comments and questions "out there" about how to change the background/wallpaper on OS X so that you have the same background image on all of your desktops/spaces and all of your monitors. The way Apple has implemented this, at least on Lion, is goofy as heck. I've been participating in one of these discussions on this [Apple Support Community thread](https://discussions.apple.com/message/15665521#15665521) and while there's been a couple of decent hacks, I've not really liked any of them so far.

I was playing with this again today, not really happy with any of the solutions I've seen. I first started looking into [python/appscript](http://appscript.sourceforge.net/index.html), which used to expose the internal bits necessary to do this, but I discovered that it's been discontinued. I did find some nice Applescript examples that led me down a different path. Here's what I've ended up with. And my apologies to the numerous people who came up with partial solutions to this... this has been cobbled together from their work, but I didn't keep track of all the parts.

This Applescript (I saved mine as ~/bin/changeBackground.scpt) will prompt you for a new background image, then it will iterate through all your spaces and per each space iterate through all monitors and set the background image. I have 8 spaces, for example, so this script will prompt me for a new background image and then switch to desktop 1, change both right and left monitor backgrounds, and then switch to desktop 2 and so on. This is only the second time I've tried playing with Applescript at all, so there's probably some things I'm not doing right, but thus far, this seems to be working better than the other options I've tried!

It's still a little goofy because it requires actually flipping through the spaces (at least it's automated!) while it changes the background for each space. And this particular implementation requires the user to manually set how many desktops they have, as well as the keybinding that takes you to desktop 1 as well as the keybinding for "move right a space". I would LOVE to see this Applescript enhanced so it doesn't require that to be changed per individual user. And this script requires "enable access for assistive devices" to be set under Universal Access.

But anyway... disclaimers aside, I'd love to hear comments, etc. =:)

> -- pick a new background image set theFile to choose file
>
>
> -- Find out how many spaces/desktops you have (this doesn't work on Lion?): tell application "System Preferences" reveal anchor "shortcutsTab" of pane id "com.apple.preference.keyboard" tell application "System Events" to tell window "Keyboard" of process "System Preferences" set numSpaces to count (UI elements of rows of outline 1 of scroll area 2 of splitter group 1 of tab group 1 whose name begins with "Switch to Desktop") end tell quit end tell
>
>
> log numSpaces
>
>
> -- the above doesn't work, apparently, so set the number of spaces/desktops manually set numSpaces to 8
>
>
> log numSpaces
>
>
> -- Loop through the spaces/desktops, setting each of their backgrounds in turn: -- *Note*: Set your keyboard shortcut for desktop 1 if it's different tell application "System Events" to key code 18 using {command down} -- Desktop 1
>
>
> repeat (numSpaces) times
>
>
> -- Now loop through each monitor (confusingly called desktop) and change its background tell application "System Events" set monitors to a reference to every desktop set numMonitors to count (monitors) log numMonitors repeat with monitorIndex from 1 to numMonitors by 1 set picture of item monitorIndex of the monitors to theFile end repeat end tell
>
>
> delay 1
>
>
> -- switch to the next desktop -- *Note:* Set your keyboard shortcut for "next desktop" if it's different tell application "System Events" to key code 124 using {command down, control down} -- ⌘→ delay 1 end repeat
