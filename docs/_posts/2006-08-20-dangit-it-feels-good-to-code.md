---
layout: post
title: DANGIT it feels good to code!
date: 2006-08-20 01:25:51.000000000 -07:00
published: true
categories:
- KDE
- Linux
- Open Source
tags: []
permalink: "/2006/08/20/dangit-it-feels-good-to-code/"
---

FINALLY took a couple of hours late, late, late tonight and looked at the pesky little kpilot bug which caused a nasty little SIGSEGV with the vcal-conduitbase::slotProcess code during a "copy handheld to PC" sync. Turns out there was a single missing set for the fNextState in the case of ConduitAction::SyncMode::eCopyHHToPC, which as luck would have it, is exactly what I was trying to do.

So, yay me on fixing that annoying buglet which was niggling at the back of my brain for the last couple of months.

Secondarily, one of: gdb, PowerPC Linux, AAP sucks donkey elbows with regards to trying to debug this problem I was having. I could not for the life of me attach gdb to kpilot's pid and get it to give me a decent backtrace, nor could I get it to set a breakpoint inside the source code for kpilot's conduit libraries!@#$@#$%!!!!! I swear this used to be possible!

Tertiarily (?), both Eclipse 3.2/CDT and Kdevelop crash ***ENTIRELY*** too often for me, making them both just about darned un-useful. Had to revert to using vi and std::cout to track down this buglet!! And I was SO hopeful that CDT would finally give me a good IDE for C++, but either I'm doing something stupid or it's still not able to resolve declarations and definitions on a consistent, useful basis.

So, in summation:

- Darnit, it feels REALLY good to get a chance to code on KDE again!
- Darnit, it was frustrating to have Eclipse/CDT and Kdevelop crash so stinking much on me
- Darnit, it's late!

Good night, Gracie.
