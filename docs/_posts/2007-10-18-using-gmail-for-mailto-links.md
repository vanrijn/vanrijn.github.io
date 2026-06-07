---
layout: post
title: 'Using Gmail for mailto: links'
date: 2007-10-18 11:57:41.000000000 -07:00
published: true
categories:
- Google
- Linux
tags: []
permalink: "/2007/10/18/using-gmail-for-mailto-links/"
---

Blame it on [Seb](http://sebruiz.net/), but I've been using Gmail's web interface lately. This is partly because I'm in the middle of another life-changing job transition (but this one I'm *really* excited about, aside from the [great white sharks](http://movingparts.net/2007/10/18/great-white-sharks-and-you/) and the triangle of death), partly because I like change (and after having used nothing but kmail for a few years now, I'm ready for a change if for nothing other than to see how we in KDE PIM land can do things better), and partly because I'm trying to keep less personal data on my work laptop. I have been using Google's Apps For Your Domain for the last year or so, and I like it much good. However, one thing that Gmail lacks is any IMAP interface whatsoever, which means that I've had a really convoluted setup going on which uses GAFYD for my MX handling, and then involves a subdomain on my regular web host server which I forward all e-mail to and subsequently access via IMAP. Ick.

([Google people](http://www.google.com/search?q=gmail%20imap&ie=utf-8&oe=utf-8&aq=t&rls=org.mozilla:en-US:official&client=firefox-a): [PLEASE](http://www.google.com/url?sa=t&ct=res&cd=1&url=http%3A%2F%2Fwww.mikeindustries.com%2Fblog%2Farchive%2F2006%2F04%2Fhow-to-use-gmail-over-imap&ei=-X4XR_vZCIOkecuQ2NMN&usg=AFQjCNFsAux7O0ZemaRJ6emT3s-5CYuwDA&sig2=c0S_YY-5wNqn3xWtP48OHA), [PLEASE,](http://www.google.com/url?sa=t&ct=res&cd=2&url=http%3A%2F%2Flifehacker.com%2Fsoftware%2Fhow-to%2Fuse-gmail-over-imap-277178.php&ei=-X4XR_vZCIOkecuQ2NMN&usg=AFQjCNH3UQy3enbYDzzUUCpIGcvqevLpNA&sig2=KOBKvrmfcofeQbddulBHqQ) [PLEASE](http://www.google.com/url?sa=t&ct=res&cd=3&url=http%3A%2F%2Fwww.downloadsquad.com%2F2007%2F07%2F11%2Fhow-to-use-gmail-over-imap-and-tag-your-mail-too%2F&ei=-X4XR_vZCIOkecuQ2NMN&usg=AFQjCNGMJiEPzxKhUSxqo7Pq2Txvy7sm4w&sig2=MmdiEAb784a6ndhG12fisg) [add](http://www.google.com/url?sa=t&ct=res&cd=4&url=http%3A%2F%2Fmail.google.com%2Fsupport%2Fbin%2Fanswer.py%3Fhl%3Den%26answer%3D10339&ei=-X4XR_vZCIOkecuQ2NMN&usg=AFQjCNFCGdQNb6f-LbHnoCQ9_SmI19B32A&sig2=JXYu1KuFMR81COqPgO8IIw) [an IMAP interface to Gmail](http://www.google.com/url?sa=t&ct=res&cd=6&url=http%3A%2F%2Fwww.petitiononline.com%2Figmail%2Fpetition.html&ei=-X4XR_vZCIOkecuQ2NMN&usg=AFQjCNGpj3ffoVlVaV9j8YmghG2_jWk5IA&sig2=1MnU6T_B8J-cj4sOR3Po-Q)!!! The workarounds suck!)

Anyway, I digress...

The second thing that irks me about Gmail's web interface is that it has no API for syncing contact information whatsoever. This absolutely sucks, but I expect that with Google trying to position itself as an online "all your information are belong to us" provider, that they'll either remedy the ridiculously bad contact handling themselves or replace it with an acquisition. Please? And let me sync it with my Palm PDA??

But back to the point, one thing that is lacking in using Gmail's web interface is the ability to click on a "mailto" link (or right-click in Firefox and do "send link"). Apparently, there are Google-provided solutions to this on OS X and Windows (Google people: please treat the Linux desktop as a first-class citizen too??) but they've not done anything for this functionality on Linux. However, I came across [this nice little HOWTO from the Gentoo folks](http://gentoo-wiki.com/HOWTO_Open_mailto:_links_in_gmail), which does the trick quite nicely. I've modified the shell script slightly to try to stop Gmail from going into some kind of a loop and not actually working if there's no recipient passed to it (like what happens when you RMB click in Firefox and do "send link"), but I'm not sure if it's something goofy with GAFYD...:

> #!/bin/sh BROWSER="firefox"
>
>
> ME=$(basename $0) DEBUG=/tmp/$ME.debug
>
>
> echo "$(date)| incoming uri: [$1]" >> ${DEBUG}
>
>
> # remove the ? and mailto from the uri and convert "subject" to "su" uri=$(echo "$1" | sed -e 's,subject=,su=,' \ -e 's,\?,\&,g' \ -e 's,^mailto:,,')
>
>
> echo "$(date)| outgoing uri: [$uri]" >> ${DEBUG}
>
>
> if [ "$uri" ]; then exec $BROWSER "https://mail.google.com/mail?view=cm&tf=0&to=$uri" fi
>
>
> exec $BROWSER "https://mail.google.com/"

[[ *UPDATE* ]] A zillion thanks to Giuseppe D'Angelo, who pointed me to the [Better Gmail](http://lifehacker.com/software/gmail/lifehacker-code-better-gmail-firefox-extension-251923.php) firefox extension. This rocks a LOT! =:) So the above shell script still has relevance for KDE/GNOME url handling, but isn't as necessary for firefox mailto's... =:)
