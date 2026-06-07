---
layout: post
title: Syncing Exchange Calendar 1-way Into Korganizer/Kontact
date: 2007-04-17 10:10:10.000000000 -07:00
published: true
categories:
- KDE
- KPilot
tags: []
permalink: "/2007/04/17/syncing-exchange-calendar-1-way-into-korganizerkontact/"
---

I've alluded to this before, but never really posted properly about it. Warning: this is very geeky...

My current employer uses Exchange as its mail/contact/calendaring solution. I have no say in the matter, so hush. =;) But this poses some challenges to those of us insisting on using Free Software at work (like me). Evolution has a connector for this, but I much-prefer KDE solutions, so I stick with Kontact and Korganizer, and of course KPilot to sync my calendars with my palm. To further complicate things, nobody in KDE PIM has the time/resources to make Kontact play nicely with Exchange as a calendar back end.

So, what I must have is the ability to keep my private and work calendars separate. Read: I do not want to be keeping my personal information on the corporate Exchange server. I also have a Palm (Treo 650 currently) PDA and I sync all of my calendar data with it and Korganizer's "std.ics" iCalendar file. Because of the fact that I insist on keeping my work and private data separate, I cannot use the otherwise possibly useful VersaMail Exchange plugin that synchronizes Mail/Calendar/Contact data for you. Also, KPilot operates best when it's synchronizing the Palm calendars with a single iCal file, so creating a separate file for korganizer to show me with my Exchange calendar is less than useful.

My approach, then is to write a wrapper process that can retrieve my Exchange calendar, tag each calendar item with a category that I only use for Exchange, and then 1-way sync my exchange calendar into Korganizer's std.ics. Oh--I also use KMail to access my Exchange mail account via IMAP, and because the current lack of built-in calendaring cooperation between KDE PIM (note: hire me to fix this!! =;) ), whenever I get a meeting request, I click the URL and open the appointment in Firefox (using Outlook Web Access). Not perfect, but certainly very functional and stable and I don't have to bring up Outlook or Windows for any of it, which makes me very happy.

My first stab at this (which has worked very well for 6+ months now) was to use OWASync (Outlook Web Access Sync) which was written by Graham Cobb. This is a TCL/Starkit-based solution. And again, this has worked well for quite a while now, but has recently stopped working for some unknown reason.

So since OWASync has been having troubles retrieving my calendar lately (and I *really* do not like TCL), I started looking for another Exchange retriever, and I found a really, really nice Ruby implementation [here](http://www.peterkrantz.com/2006/exchange-to-ical-http/). It's based on the [RExchange project](http://rubyforge.org/projects/rexchange/), and provides a nice and very easy to understand front-end script. I've never touched Ruby before this, but I've been playing with this script (adding some missing fields like appointment status, location, and description) and I am hooked! Ruby is very cool. And the thing I like best about this approach over the TCL/Starkit one is that I can easily modify and test this Ruby stuff and feel confident that I know what I'm doing.

So to put it all together, I have [a shell script](/bin/exchange_calendar_1way_sync.sh) that I have crontabbed to run every 10 minutes. This shell script calls [my modified Ruby script](/bin/rexport-events.rb) which pulls down my Exchange calendar (VERY quickly) and creates a single file which has all of my calendar items in it. As it creates the file of events, I have it adding on my custom "Exchange-only" category (CATEGORIES:WorkXChange) to each event. I do this so that my shell script can clean up all previously 1-way-synced Exchange items from my korganizer iCal file, and so that I can also associate a color with this category in both korganizer and my Treo so that I can easily see which items in my calendar are work-related. If the calendar retrieval was successful, my shell script then saves off a copy of my korganizer's std.ics file, removes all events which have "WorkXChange" in it, and then adds in all of my just-download Exchange events. It also reports on how many events were there before and after the changes so that I can easily tell if something is going wrong. And it does some sanity-checking before overlaying korganizer's std.ics file to make sure that it hasn't been changed since it grabbed a copy of it. Korganizer will recognize that its file has changed and reload the calendar automatically. And KPilot will remove the previous Exchange events and add the new ones for me as well.

Perhaps not quite as seamless as one might like, but until I (or some other fearless KDE-PIMster) find the time to start getting Kontact to play nicely with Exchange's calendaring stuff, it most certainly does the trick. HTH!! =:)

**UPDATE** : I've discovered another really cool ruby library called simply enough [iCalendar](http://rubyforge.org/projects/icalendar). It does a very nice job of dealing with iCalendar files. So I've completely re-done the merging as I have posted it above and now use 1 shell script that calls 2 ruby scripts

- [rexport.rb](/bin/rexport.rb) which does the exchange OWA calendar retrieval and iCalendar output
- [calmerge.rb](/bin/calmerge.rb) which uses the [iCalendar ruby library](http://rubyforge.org/projects/icalendar) and harvests old X-PILOTIDs from korganizer's file, then removes the last-synced Exchange events, then merges in the just-downloaded events.

Much more better. But I'll leave the old, crufty shell/perl method as it is above too... =;)

**UPDATE Part Deux : **I wanted to add ATTENDEE and ORGANIZER retrieving to my Exchange download/merge process. I hacked it easily enough into [rexport.rb](/bin/rexport.rb) and [rexchange/appointment.rb](/bin/appointment.rb), so my Exchange calendar download process works correctly. However, I couldn't for the life of me get the Ruby iCalendar library to deal with the multiple-occurences-per-VEVENT ATTENDEE tag correctly. So I did what I should have done to begin with (although learning Ruby was REALLY cool) and wrote a simple C++ program that uses KDE PIM's libkcal library to handle the calendar merging for me. And it works MUCH better and MUCH faster now. You can find [mergecalendars.cc](http://websvn.kde.org/branches/KDE/3.5/kdepim/kpilot/tests/mergecalendars.cc?view=log) in [kpilot's tests directory](http://websvn.kde.org/branches/KDE/3.5/kdepim/kpilot/tests/), in which you'll also find the CMakeLists.txt for it. You'll also need to have kdepim and kdepim-dev installed on your machine to build mergecalendars.cc.

So, hopefully this is the last update to this post, and hopefully this will come in nice and handy for someone else who wants to be able to view their Exchange calendar in kontact. Granted, I've twisted this to a larger scale than most people would need to because of how I wanted to keep my private data out of the Exchange server, and I want to sync it all reliably with my Treo 650 via KPilot. [Here's a tarball](/bin/exchange-download-and-merge.tgz) of the whole thing (make sure you right-click and choose save-as). I'd love to hear from anyone who is looking to do what I've done here and please let me know if this does or does not help you in your travels, oh weary Exchange sojourner.

**UPDATE Part Trois** : [Here's the latest skinny](http://movingparts.net/2008/04/09/kpilot-hackery-of-sorts-or-how-to-sync-your-works-exchange-calendar-to-your-palm-part-iii/), thanks to Exchange 2007, grr...
