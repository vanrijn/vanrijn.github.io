---
layout: post
title: how you say, 'filing cabinet'?
date: 2002-01-10 23:21:00.000000000 -08:00
published: true
categories:
- Life in General
tags: []
permalink: "/2002/01/10/how-you-say-filing-cabinet/"
---

Well, I used to have a section here about a patch I contributed to gkrellm to allow it to comfortably rest inside blackbox's "slit" (think dock/wharf), but since gkrellm 0.9.7, it's been accepted into gkrellm's source. I guess I won't mention it after all... Er. Wait... =;)

I've written a shnazzy little utility (perl script) for use with the blackbox window manager. Download this [little beauty](/bin/background_menu.pl) and automagically create blackbox menus from a hierarchy of image-directories. That is, this script will do it all for you. It will organize your backgrounds into two main submenus (those in themes and those not), and will create submenus from the directories it finds (just tell it where to look) and menu items that when clicked in blackbox will set your background image in X. It's decently-self-documented, so [download it](/bin/background_menu.pl) and give it a whirl. =:)

This next one isn't so much use to me now that I've gone to using Maildir-format for my mail in *nix. The problem used to be that I get bored quickly. =:) Well, that's still a problem. But I used to switch between kmail, mutt, balsa, sylpheed, evolution, etc., etc., and they made a mess out things. Of particular nuisance to me was the interplay between evolution and mutt. So [this perl script](/bin/evolution_to_mutt_links.pl) runs through a directory you point it at (documentation in the script itself) and it will create you a hierarchy of symlinked mbox files for use with mutt. As I said, I've switched to using Maildir format, so mutt and evolution can both access the same files with no problems whatsoever. I used this perl script ([mb2md-date-sh.pl](/bin/mb2md-date-sh.pl)) that I found on the 'net somewhere to convert my 8+-year-old mbox directory structure to a Maildir format. And (also of no use to me since I use Maildir now) here's a script ([mbox_to_evolution.sh](/bin/mbox_to_evolution.sh)) I found to convert an existing mbox-directory tree to an evolution mbox tree.

I use evolution for my main e-mail client nowadays, and [this little quickie](/bin/evomail.sh) allows you to set evolution up in opera (and anything else) as your e-mail client. It's called [evomail.sh](/bin/evomail.sh).

I would be absolutely lost without my Palm Pilot. =:) I currently rely on a IIIc to hold my entire life in its 8-meg body. This perl script ([mpadq](/bin/mpadq)) (which I didn't write) has proven itself extremely useful to me. I use it in mutt to parse the contents of my jpilot-controlled palm Addressbook for address lookups. I've also written a few hacks based on it for creating alternative address book formats from my palm's contents. Since I use evolution now and it does everything I need it to (including syncing with my Palm), these are pretty useless now-a-days. But here they are anyhow.... ([pilot_to_kmail.sh](/bin/pilot_to_kmail.sh)) is simple little shell script that will create a "kab" addressbook for use in kmail from the output of the above mpadq program. My second iteration of this was ([jpilot_to_address.pl](/bin/jpilot_to_address.pl)), which is a modification of the mpadq script itself. It accepts command-line arguments and will happily give you either a "kab" kde-addressbook or a "gnomeCard" addressbook from the contents of your palm pilot.
