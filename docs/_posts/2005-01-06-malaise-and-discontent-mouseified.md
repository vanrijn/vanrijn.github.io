---
layout: post
title: Malaise and discontent, mouseified
date: 2005-01-06 14:51:20.000000000 -08:00
published: true
categories:
- Life in General
tags: []
permalink: "/2005/01/06/malaise-and-discontent-mouseified/"
---

Just wanted to post an update to my rant yesterday about getting cursors working, etc. I was up until 2 in the morning last night, wracking my brains about how to get a simple drop-shadow to work in [perlmagick (ImageMagick-perl interface)](http://web.archive.org/web/20050325051755/http://www.imagemagick.org:80/www/perl.html). Very grumpy this morning as a result and feeling in general rather bad. And the worst of it was that I couldn't figure it out. ImageMagick is probably the most confusing and simultaneously powerful interface that I've yet come across. Anyway, at the end of it, instead of trying to get the perl modules to do what I wanted it to, I've cheated and used a system() call from the perl script to get the job done. And it works nicely.

In case you tuned in late, there is a nifty little perl script called sd2xc.pl that converts StarDock/CursorXP neato animated cursors into cursors that X and Linux and UNIX and *BSD, etc., can use. Well, this has all worked wonderfully until a recent upgrade to ImageMagick which broke the image compositing and alpha-channel stuff.

So, without further ado, I give you my ugly hack around the ImageMagick API changes:

- [convert_cursorXPthemes_to_XC.sh](/bin/convert_cursorXPthemes_to_XC.sh) : shell script that iterates through a directory of zip-files (named .zip, which contains one or more .CurXPTheme files, each of which are simply a zipfile.
- [sd2xc.pl](/bin/sd2xc.pl) : my ugly hacks/fixes to sd2xc.pl.  This requires the latest [ImageMagick](http://web.archive.org/web/20160317190748/http://www.imagemagick.org:80/www/download.html) programs (6.1.7 right now).  This perl script will do the actual conversion work and add drop-shadows if desired to the CursorXP cursors.  If someone knows how to do what I've done:
> system("convert -page +$shadowx+$shadowy $outfile  \( +clone -background black -shadow 80x4+$shadowx+$shadowy \) +swap -background none  -flatten -crop +$shadowx+$shadowy $shadowfile");
  in straight perlmagick, then PLEASE tell me how, as it would be much more efficient to do it that way.
- [cursors_cleanup.sh](/bin/cursors_cleanup.sh) : simple shell script which cleans up multiple images of the same cursor and uses symlinks instead.

I'm still grousing about all the hoops and dance moves one has to do to get things like this working in Linux/X/UNIX, but at least I have some new pretty cursors to keep me distracted for a month or so.

Again, I repeat, IF ANYONE KNOWS HOW TO DO THIS BETTER, PLEASE TELL ME.

=:)
