---
layout: post
title: Cpanel Web Host and IMAP Email Filtering
date: 2006-12-05 01:29:29.000000000 -08:00
published: true
categories:
- Life in General
tags: []
permalink: "/2006/12/05/cpanel-web-host-and-imap-email-filtering/"
---

I wish I would have found [this very helpful post](http://forums.cpanel.net/showpost.php?p=50826&postcount=70) a long time ago, but such is life, I suppose. I've been trying to figure out a good way to do server-side filtering on my cpanel-based IMAP server for quite a while now, but hadn't found anything official. I wrote some custom exim filters that my last web host was gracious enough to let me put in place, but that was a little hackish, since it required a good-natured web-hosting admin.

But following Pda0's suggestions from [his post](http://forums.cpanel.net/showpost.php?p=50826&postcount=70) seems to be working quite well thus far. I'll quote him below...

> I've been able to set up procmail in a per-user basis, not globally! The .procmailrc is global to a domain though.
>
>
> Let me rewrite the steps:
>
>
> 1.- Get into Cpanel and make a forwarder to a user (lets say [tom@domain.com](mailto:tom@domain.com)), that forwards tom's email to |/usr/bin/procmail
>
>
> 2. Repeat 1.- for each user you want to set up to use procmail
>
>
> 3.- Make a .procmailrc as in /home/domain.com/.procmailrc
>
>
> 4. procmailrc then will be called each time some user configured in 1.- gets mail, AFTER exim has done all its work.

Pretty slicque!! Works too!! =:)

**UPDATE:**

I did in fact get this working, though it was a little bit more complex than I thought it would be. First of all, the reason I have to use procmail in addition to the standard exim is that my webhost (hostgator) is using a really cool upgraded version of cpanel that finally does Maildir mailboxes (as opposed to the older and scarier mbox). So, if that was not the case, then you could use only cpanel's built-in mail filtering dialog, and for the "destination" text field, just give an mbox name to put the mail in (with full path).

So, what I needed to do is for a single user on my domain, I need to be able to filter incoming mail into Maildir IMAP mailboxes. For instance, all KDE-related mail (mailing lists, etc.) should go in USER/.code.kde/, all pilot-link mailing list mail should go in USER/.code.pda/, etc. (it's a courier IMAP server). What I tried to do first for this was use cpanel's built-in e-mail filtering (Mail Manager Main Menu | Email Filtering in cpanel) and assign mailboxes for some filters. This doesn't work because cpanel/exim isn't configured correctly to write filtered mail to Maildir destinations.

Next idea: use the email filtering dialog from cpanel to send all e-mail to USER off to procmail for processing and then use procmail filters to do the Maildir writing. Now, the way that cpanel's email filters work is that they get written out to ~/.filter on your web host. Whenever you make a change to your filters through cpanel, that file is parsed and is used to generate /etc/vfilters/YOURDOMAIN, which is a standard exim format file. What this means is that even if cpanel's built-in exim filters don't work for you (cpanel only provides 6 filter expressions), you can use your own as long as it's a valid exim filter expression. This is what I ended up having to do.

So, my first crack at this was to make a cpanel email filter for "To:" with my USER. The problem is that cpanel actually uses exim's $h_to: filter, which ONLY looks at the "To:" header in the e-mail. This doesn't work for mailing lists because the destination (the $h_to: or header To:) is kde@mail.kde.org (for example) and not my e-mail address. It turns out that the correct way to ask exim to tell you who it's going to deliver the e-mail to is the $local_part: filter. But you can't select that from cpanel's filter list, now can you?

To get around this, simply download your ~/.filter file, edit it and re-upload it to your server. You will then have to make another change in cpanel's email filtering dialog so that it writes your changes to /etc/vfilters/YOURDOMAIN where exim will be looking for filtering rules. The easiest thing to do is just add a new filter for Subject: "wibblewibblewibble" with action of "|/usr/bin/echo" or something silly. Add that (or any filter) and then remove it and what you'll end up with is the filter that you manually added to ~/.filter written correctly to /etc/vfilters/YOURDOMAIN and exim should use it.

There's a couple of other options I could have taken with this, certainly, such as asking hostgator to allow me to manage my /etc/vfilters/YOURDOMAIN (which I did on my old host), or setting up a forwarding rule instead of a mail filter rule, but this seems cleaner, etc.

Anyway, here is my ~/.filter file:

${lc:$local_part} contains "vr"+++++++|/usr/bin/procmail
... and here is my ~/.procmail file:

PATH=/bin:/usr/bin:/usr/bin:/usr/local/bin
ORGMAIL=$HOME/mail/YOURDOMAIN/USER/
MAILDIR=$HOME/mail/YOURDOMAIN/USER      #youd better make sure it exists
DEFAULT=$MAILDIR/   #completely optional
LOGFILE=$HOME/.procmail.log   #recommendedVERBOSE=yes
DELIVER_TO = `formail -czxDelivered-To:`BACKUP=".backup/"
BLACKBOX=".code.blackbox/"
KDE=".code.kde/"
PDA=".code.pda/"
OPERA=".code.opera/"
# backup mail for safety :0 c $BACKUP

# blackbox... :0 * ^Subject:.*blackbox $BLACKBOX

:0 * ^TOblackbox $BLACKBOX

# kde... :0 * ^Subject:.*kde $KDE

:0 * ^TOkde $KDE

# pda... :0 * ^Subject:.*opensync $PDA

:0 * ^TOpilot $PDA

# opera... :0 * ^TOopera $OPERA

# mail to USER goes here... :0 * $DELIVER_TO ?? ^^USER@YOURDOMAIN $DEFAULT

Hope this helps the next poor soul who tries to do server-side IMAP filtering on a cpanel-based web host. =:)
