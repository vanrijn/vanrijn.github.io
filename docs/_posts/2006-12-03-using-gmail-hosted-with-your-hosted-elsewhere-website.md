---
layout: post
title: Using GMail Hosted With Your Hosted-Elsewhere Website
date: 2006-12-03 23:44:51.000000000 -08:00
published: true
categories:
- Google
- KDE
- Life in General
tags: []
permalink: "/2006/12/03/using-gmail-hosted-with-your-hosted-elsewhere-website/"
---

I fought this stupid thing for a good few days with no luck (and loss of sleep, etc.) and I finally [found the solution](http://groups.google.com/group/hosted-mail-delivery/browse_thread/thread/ba377001d13a3fd7/00ec7ab987fab42f?lnk=gst&q=550+Sender+verify+failed&rnum=2#00ec7ab987fab42f).

I'm using Google's Apps For Your Domains as the e-mail server for my domain. First, there's the 2 gigs of storage per user. Also, it's a nice solution for long-term backup and storage. And I'm most interested in using GMail's spam filters and spam training, since that's one thing that is VERY non-simple (non-possible, honestly) with every web hosting solution I've seen yet.

Unfortunately, GMail doesn't allow an IMAP interface (yet, hopefully?? come ON gmail guys!!!). I check my e-mail from multiple machines and POP3 is very unsuited for this purpose (even with the recent:username@ hack which is admittedly interesting). And I just cannot bring myself to using only GMail's web interface. Call me old-fashioned or whatever, but I just can't do it. I like being able to use KDE's excellent PIM applications to manage my mail, contacts, and calendars--and most importantly, sync it all up with my PDA with kpilot. So what I wanted to do was bring the e-mail that I have coming into my GAFYD GMail account into my web host's IMAP server. Such a simple thing to do, I thought.

I was horribly wrong.

I've tried a couple of routes to do this. My first thought was that I could use GMail's auto-forwarding to push incoming e-mail onto the IMAP server. So I set up a sub-domain that I'd ask my web host to handle mail for and forward all e-mail from GMail to it. The problem was that for some reason I was getting errors like this:

> This is an automatically generated Delivery Status Notification
>
>
> Delivery to the following recipient failed permanently:
>
>
> [email address]
>
>
> Technical details of permanent failure: PERM_FAILURE: SMTP Error (state 9): 550-Verification failed for < [email address]> 550-No Such User Here 550 Sender verify failed

But I couldn't tell where things were failing. So I started looking at other options.

I tried running fetchmail on my web host and popping mail from gmail into my IMAP server. But unfortunately, my web host doesn't allow outbound POP+SSL, so that doesn't work. It also rules out things like using Horde+IMP to fetch mail too. I then tried running fetchmail on my home machine, popping mail from GMail and then forwarding e-mail to my web host's IMAP server, but my web host doesn't allow forwarding from my IP address (it knows it's from a home cable provider). So I went back to looking at the subdomain forwarding problems.

Turns out (thankfully I found [this post from a guy with the exact same problem](http://groups.google.com/group/hosted-mail-delivery/browse_thread/thread/ba377001d13a3fd7/00ec7ab987fab42f?lnk=gst&q=550+Sender+verify+failed&rnum=2#00ec7ab987fab42f)) that the problem was that my web host was trying to verify the username that was being forwarded. Now, the funny thing is that GMail doesn't just forward for user@domain. I tacks gunk on in the middle, so that what it turns out to be is user+caf_user=subdomain@domain. So my web host tries to verify that e-mail address, which obviously doesn't exist in the user accounts that it knows about. The problem was that my web host used to be handling my e-mail for my domain, so it was looking internally to verify that e-mail address. The solution, as noted in that post, was to tell my web host that it was not handling e-mail for my domain by changing its MX records to GMail's MX handlers.

Simple enough solution. And things seem to be working swimmingly since I fixed that. HTH somebody else out there. =:)
