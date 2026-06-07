---
layout: post
title: Korganizer, Exchange, OWASync, Google Calendar, KPilot
date: 2008-11-21 13:01:12.000000000 -08:00
published: true
categories:
- KDE
tags:
- KDE
- PIM
permalink: "/2008/11/21/korganizer-exchange-owasync-google-calendar-kpilot/"
---

I use KOrganizer to view and manage my personal calendar. My employer uses Microsoft Exchange *spit* for its calendaring solution, so I also have a calendar on the Exchange server that holds all of my work meetings and reminders. I would really like to keep everything on my Google Calendar too, so I can share it with my family. And I sync everything with my Palm so I can carry my schedule with me and get alarms when a meeting is coming up. As an aside, I'd really like to use my Nokia N810 for this instead of my Palm, but alas this is just not there yet, mCalendar notwithstanding.

So my current "solution" involves using OWASync to pull down my Exchange calendar, crontabbed shell scripts plus some KDE ical code to 1-way-merge it into my personal calendar, a constantly-running GCalDaemon that takes it all and merges it in with Google Calendar, and KPilot which does its own merging with my KOrganizer std.ics file. Um. Yuck! This sucks! And there is weirdness that happens betwixt all the moving parts when anything non-standard happens, like updated Exchange meetings, timezone translation, etc., etc. And I'm pretty sure it's not going to work with KDE4 and Akonadi being that all of this is operating directly on the raw ics files. And I guess that's the real answer, eventually--Akonadi--however, I don't believe that all the pieces are there yet. *sigh*

Does anyone have any better solutions for this? The biggest missing pieces seem to be:

- PIM (Calendar, Contacts, ToDos, Notes) software that syncs with a Linux desktop (or hell, even Google resources directly) for the Nokia N810/Maemo.
- A KDE bridge for Exchange.
- A KDE bridge for Google Calendar/Contacts/etc.

*grouse*
