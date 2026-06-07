---
layout: post
title: Training spamassassin from a cpanel-based webhost
date: 2004-12-15 08:49:59.000000000 -08:00
published: true
categories:
- Life in General
tags: []
permalink: "/2004/12/15/training-spamassassin-from-a-cpanel-based-webhost/"
---

Just to answer my own question, sort of, [I've found this](http://www.lunarforums.com/forum/viewtopic.php?t=13960).

which turns out to be very useful. It's not quite as automatic as I would like, but it seems to work. In case the page is moved/removed/whatever, I'll paste some of it here...

> Assumptions - that you know how to log in to CPanel - that you know how to use Outlook, or know how to configure your Email client based on my descriptions of using Outlook, to add an IMAP account - for these examples, the LunarPages account name is lpaccount and password is lppassword ; your domain name will be mydomain.com ; I'll do my best to keep those colors used throughout this text to highlight where you'll need to insert your own information.
>
>
> Terminology SPAM: unsolicited Emails that you've received that want you to buy something or contain adult-themed references that you'd rather not get anymore. HAM: non-spam, legitimate Emails SA: short for SpamAssassin
>
>
> Getting Started Generally speaking, there are a handful of steps to follow to get this working: 1. set up IMAP folders to hold spam and ham messages 2. set up an IMAP account in Outlook if you so choose 3. set up your SA user_prefs file 4. build the training Perl script 5. learning how to run the script 6. closing notes and suggestions 7. more thoughts on SpamAssassin
>
>
> 1. Set up IMAP folders to hold spam and ham messages - log in to cpanel - click on the mail icon - click on the 'spam assassin' link - click on the button to 'enable spam assassin' - click on the button to 'enable spam box'
>
>
> - click the 'home' link at very top of the screen
>
>
> - click on the 'webmail' icon - click on the 'squirrelmail' link - click on the 'folders' link *snip* - also in the 'folders' screen, towards the top, you should be able to create new folders under a heading called 'create a folder' - create a folder called "myham" under the subfolder of 'none' - create a folder called "myspam" under the subfolder of 'none' - click 'refresh folder list' on left frame again, and you should see 'myham' and 'myspam' in the list
>
>
> 2. Set up IMAP in Outlook to manage these mailboxes *snip* basically, this is very-well documented in the linked page and I won't repeat it here. Suffice it to say here that the goal is to copy HAM (not SPAM, but mistakenly identified as SPAM) into the "myham" folder and missed SPAM into the myspam folder through your e-mail client.
>
>
> 3. Set up SpamAssassin's preferences file: user_prefs SA has a configuration file that you should have accessible to you in your CPanel file manager.
>
>
> In CPanel: - click on the File Manager icon - should see a folder called /.spamassassin/ - click the folder icon beside it to move into that folder - you should have 3 files in there:
>
>
> Quote: bayes_toks holds data about various elements it has seen from messages from previous scans; this information includes where the message came from, the route it took to get to you, when the message was sent, who it was from, who it was to, the subject line, other headers, and elements within the body of the message itself bayes_seen holds data about which messages it has looked at in the past user_prefs is the configuration file we're going to edit
>
>
> - click on user_prefs link to change the menu on the upper-right side of the screen, and click on 'edit file' from that menu
>
>
> - here is what i have set in my configuration file, you will need to modify a few elements in this file:
>
>
> Quote: required_hits 5 rewrite_subject 1 subject_tag {SPAM} bayes_path /home/ lpaccount /.spamassassin/bayes bayes_file_mode 0600 bayes_ignore_header X-MailScanner bayes_ignore_header X-MailScanner-SpamCheck bayes_ignore_header X-MailScanner-SpamScore bayes_ignore_header X-MailScanner-Information
>
>
> - save the file and close the window that CPanel opened for you to edit that file - go up one level in the file manager - go into public_html - go into cgi-bin - click on the link to 'create a new file' - call it "sa-learn.cgi" (no quotes) - here are the contents of the file:
>
>
> #!/usr/bin/perl
>
>
> my $salearn = "/usr/bin/sa-learn" ; $| ;
>
>
> print "Content-type: text/plain\n\n" ;
>
>
> print "Learning SPAM:\n" ; print `$salearn -p /home/lpaccount/.spamassassin/user_prefs --mbox --spam --showdots /home/lpaccount/mail/myspam` ; print "\n\n" ;
>
>
> print "Learning HAM:\n" ; print `$salearn -p /home/lpaccount/.spamassassin/user_prefs --mbox --ham --showdots /home/lpaccount/mail/myham` ; print "\n\n" ;
>
>
> exit ;
