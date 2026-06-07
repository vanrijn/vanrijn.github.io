---
layout: post
title: The Night of the Terrible 406s
date: 2006-03-03 08:38:58.000000000 -08:00
published: true
categories:
- Life in General
tags: []
permalink: "/2006/03/03/the-night-of-the-terrible-406s/"
---

I have not been able to do the "blog this" thing from Flickr for a while now. Irritating. I finally had enough of it tonight, so after a few minutes Googling, I found that some hosts are blacklisting xmlrpc.php and sending back 406 errors intentionally because of security problems with old versions of xmlrpc.php/WP that people haven't bothered upgrading/fixing/patching. To get around it, all you have to do is copy your xmlrpc.php script to some other name and tell Flickr to use that endpoint instead.

Which reminds me, I need to upgrade to the new 2.x WP release, when I get a spare couple of hours (yeah, right)....

[update]: Yikes. Just as I was trying to post this entry, I got bit by the 406 error on the wp-admin/post.php page too. Sheesh. So then I tried to submit a help desk ticket and guess what I got.... Yep, another 406 error.

Powered by [Bleezer](http://www.bleezer.com)
