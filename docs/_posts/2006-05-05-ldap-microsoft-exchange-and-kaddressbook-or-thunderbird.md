---
layout: post
title: LDAP, Microsoft Exchange, and KAddressBook or Thunderbird
date: 2006-05-05 11:37:34.000000000 -07:00
published: true
categories:
- KDE
- Linux
- Open Source
- Work Stuff
tags: []
permalink: "/2006/05/05/ldap-microsoft-exchange-and-kaddressbook-or-thunderbird/"
---

My current employer uses Exhange 2003 as its current groupware solution. I have on-and-off-again been beating my head against the proverbial concrete wall in trying to get it to work nicely with [LDAP](http://www.intranetjournal.com/foundation/ldap.shtml) and addressbooks other than Evolution or Outlook, for obvious reasons. Today, my geeky noggin' has broken through the proverbial concrete wall and I now have both [KDE's kaddressbook](http://www.kontact.org/) and [Thunderbird's](http://www.mozilla.com/thunderbird/) address book successfully using the Exchange server here at work.

Yay, me!

Two things I've found this morning that have helped my noggin' and I'll list them here for future reference for myself as well as in hopes of helping some other poor concrete/geek/proverbial/noggin'-banging soul.

First, I've found [this post](http://forums.msexchange.org/m_30659100/tm.htm) which lists a very helpful step-by-step approach for getting things almost working:

> OK, here is how Mozilla/Thunderbird LDAP works with Exchange 2000-2003:
>
>
> 1. The default LDAP port for Active Directory is 3268 (not 389) so make sure you've got this port open thru the firewall, and make sure to configure it in your LDAP account settings in Mozilla/Thunderbird.
>
>
> 2. For Base DN, you MUST enter something like dc=yourdomain,dc=com (whereas Outlook Express lets you get away with putting NULL).
>
>
> 3. For Bind DN, you must enter a domain user which has permission to search the directory. You should enter it qualified by the NetBIOS domain name, for example: mydomain\username
>
>
> 4. For some reason, Thunderbird doesn't always seem to recognize that it needs to log on before querying. The easiest, most reliable way I have found to force it is to go to the Offline tab in the Directory Server Properties and click the Download button. This function seems to "see" that Active Directory wants a logon, so Thunderbird will display the logon dialog to let you enter your domain credentials. For the username, specify exactly the same thing you put into Bind DN.
>
>
> 5. Results are returned asynchronously to the Thunderbird Address Book, so you might see "No matches found" immediately after clicking the Search button. Wait a few seconds, and your results should show up.
>
>
> 6. Mozilla and Thunderbird default to a Search Filter of (objectclass=*) which will return lots of useless (non-email address) entries from Active Directory. You can override this with something like (objectclass=person) on the Advanced tab of Directory Service Properties. Depending on what kinds of addresses are in your Active Directory, you may need to refine this filter more (for example, if you've got mail-enabled Public Folders which you want to display).
>
>
> 7. The Address Book UI in Thunderbird is just clumsy. You CANNOT search an LDAP directory by simply selecting it on the left hand side and then entering your search in the "Name or Email contains" textbox. You MUST click the Advanced button to define an LDAP search. After you find your desired address(es) in LDAP, you "should" be able to copy it to your local addresses but the stupid UI only lets you look at the Properties or add it to the recipient list for a new message (by clicking the Write button).

And then there's [this page](http://forums.mozillazine.org/viewtopic.php?p=2232464&) that helped me finally get it all working:

> You can add a new address book with the following properties:
>
>
> General tab:
>
>
> Name: ... Hostname: Base DN: dc=company,dc=com Port number: 389 (non-secure) or 636 (secure) Bind DN: YOURWINDOWSLOGONDOMAIN\yourwindowslogonuser
>
>
> Advanced tab:
>
>
> Don't return more than [ 100 ] results Scope: Subtree Search filter: (objectClass=person)
>
>
> If your organisation is large you may have to change the Bind DN so it only returns your unit (e.g. ou=yourdept,dc=company,dc=com) as otherwise Thunderbird may decide to act a bit strange.
>
>
> You can force a read by clicking the Download Now button on Offline tab, although you won't see any contacts afterwards, you have to search in the Compose window.
>
>
> If you still get no joy you can download and install Windows Server 2003 Service Pack 1 Support Tools and run ldp.exe against the exchange server. You don't even need to install it if you decompress with WinRAR (or possibly WinZip) and look for the executable.
>
>
> [http://support.microsoft.com/kb/892777](http://support.microsoft.com/kb/892777)
>
>
> That way you can find out the Bind DN and search filter. First use Connection > Connect against the server, then Connection > Bind with your user and password then use View > Tree with a blank string and you can find a tree view of your Base DN and go into departments and retrieve user data to find out their objectClass if it's not person.
>
>
> Finally in Tools > Options > Composition > Addressing tick Automatically add outgoing e-mail address to my [ Collected Addresses ] as it's much faster than searching the server.

Granted, these are instructional in getting Thunderbird to work with Exchange, but the same applies to KDE's kaddressbook.

In general, I think the sticky wicket that really got things working for me was using Microsoft's ldp.exe tool to browse the Exchange LDAP tree and see its innards. Specifically, I had to do this:

> server: [active directory server] base dn: CN=Users,DC=XXX,DC=XXX,DC=com (important to start with Users for me!!) port: 389 bind dn: [windows domain]\[username] search filter: (objectclass=*) scope: subtree

The trick was, I think, that I had to provide a more specific base dn to the address books.

Hope this helps someone else out there, wherever your geeky proverbial concrete-bashing noggin' may find you. =:)
