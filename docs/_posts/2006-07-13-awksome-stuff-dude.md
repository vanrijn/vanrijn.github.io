---
layout: post
title: Awksome Stuff, Dude!
date: 2006-07-13 10:52:50.000000000 -07:00
published: true
categories:
- Life in General
tags: []
permalink: "/2006/07/13/awksome-stuff-dude/"
---

I had need to convert some files today from being newline-separated (one line per file, key-value pairs) to '###'-separated. In other words, instead of this:

> foo=bar smith=wibble neo=smith

I needed this:

> foo=bar###smith=wibble###neo=smith

My first inclination was to try using tr solely like this:

> cat $file | tr "\n" "###"

This resulted, however, in only one "#" being used to join the lines. Not quite what I wanted. My next thought was sed:

> cat $file | sed 's,\n,###,g'

But that didn't work at all. So, my good friend Mr. Google and I were just starting to look into the deeper mysteries of sed when I found this [little newsgroup posting](http://groups.google.com/group/comp.unix.shell/browse_thread/thread/734c635252e63a2b/571747b595c947fd?lnk=st&q=sed+unix+newline&rnum=5&hl=en#571747b595c947fd) which opened my eyes to some of the magic of awk:

> cat $file | awk '{printf("%s###", $0);} END {printf("\n")}'

That's just sweet! Incidentally, I did figure out how to do it with a combination of tr and sed (convoluted because of the missing \n at the end):

> F=$(cat $f | tr "\n" "_" ); echo $F | sed 's,_,###,g'

But it's not nearly as pretty. =;)
