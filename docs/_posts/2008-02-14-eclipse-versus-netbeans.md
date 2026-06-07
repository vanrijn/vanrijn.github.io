---
layout: post
title: Eclipse versus Netbeans
date: 2008-02-14 00:28:24.000000000 -08:00
published: true
categories:
- Life in General
tags: []
permalink: "/2008/02/14/eclipse-versus-netbeans/"
---

Now, this one I'm really speaking out of the side of my head on... This is totally based on first impressions of NetBeans, albeit after 3<x<5 hours have been invested in said first impressions... I've been using Eclipse and CDT for a while for my day job at VMware (which, by the by, totally rocks!!!). And for the most part, Eclipse+CDT really does a nice job at helping me maneuver around our very large code base and lowering the learning curve after I've figured out how to teach it about include paths that it can't figure out on its own. As a C++ IDE, it's very nice, responsive, stable, and it definitely helps in learning the code base via being able to quickly search, view inheritance hierarchies/object references, and quickly take you to definitions/declarations/usages. I had an itch to scratch with VIM keybindings and from what I've seen, viPlugin fits the bill very nicely. In fact, I've just today broken down and sent off my $21 for the wee beastie. In response to a previous blog of mine, someone suggested that I look at NetBeans and SunStudio (which is built atop NetBeans) as alternatives to Eclipse as a C++ IDE, so I took some time to learn and explore today. I am definitely impressed with NetBeans in general, and their attention to C++ as a core component (as opposed to Eclipse, which provides C++ as a plugin, albeit a much-more-core plugin than previous). And NetBeans does a much nicer job, imho, in UI clarity as well as getting up and running quickly. Very nice attention to detail, and very good online help. I was up and running with our very large code base in NetBeans almost immediately--orders of magnitude quicker than doing the same thing in Eclipse. And then I tried to set up NetBeans' Code Assistance. For 4+ hours, on and off (each iteration took a painfully long time to discover that I'd still not gotten it right). Now... to be fair, it sure seems like NetBeans has some nice sophistication here, and gives you 3 ways of discovering how to construct your code model and code assistance goodness:

1. Examining a binary (depends on compiling with CFLAGS/CXXFLAGS="-g3 -gdwarf-2", iiuc)
2. Examining a bunch of build output/shared object code (also depends on compiling with CFLAGS/CXXFLAGS="-g3 -gdwarf-2", iiuc)
3. Finding its way through a mess of C/C++ source/header files (this is what Eclipse/CDT does, I think?)

However, try as I might, no matter how I told the code assistance wizard to do its thing, it only ended up finding 31 C (not even C++) files. Needless to say, no code assistance or navigability joy was mine, which makes this fantastic IDE... much less than useful for me, unfortunately. One other thing that gives Eclipse a thumbs-up here is the Perforce plugin for Eclipse. I don't think one exists for NetBeans 6. And I personally much-prefer the speed and good looks of SWT over Swing, which gives Eclipse another ++. So, all in all, I REALLY do like NetBeans. I will have to poke at it some more later, and would LOVE it (dear LazyWeb) if someone could point me in the right direction to getting Code Assistance working. But for the time being, I think I'll stick with Eclipse+CDT+VIM keybindings.
