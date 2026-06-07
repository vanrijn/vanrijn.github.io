---
layout: post
title: Google Video Player For Linux
date: 2006-06-16 00:36:23.000000000 -07:00
published: true
categories:
- Google
- Linux
tags: []
permalink: "/2006/06/16/google-video-player-for-linux/"
---

Got your attention, did I?

I run Linux on my Apple G4 Powerbook, which means that I don't have the luxury of such niceties as... oh, I don't know... *FLASH***!?!?! ** So I was happy to find that even though I can't view Google Video's Flash-based movies, I can easily enough still play them on my G4 Powerbook running PPC Linux. I whipped up a very simple and quick little script for it, as follows:

> #!/bin/bash
>
>
> PLAYER=kaffeine
>
>
> INFILE=$* TMPFILE="/tmp/$(basename $0).tmp" echo "got->${INFILE}< -... going to work..." cp "${INFILE}" "${TMPFILE}" URL=$(grep 'url' ${TMPFILE} | sed 's,url:,,' )
>
>
> ${PLAYER} "${URL}"

I then saved in in ~/bin/google-video-player.sh and chmod +755'd it. I then clicked on the download link on google video's pages, told Konqueror (or Firefox, Opera, etc., etc.) to open the file with my little script, and sat back and enjoyed as kaffeine (or xine or whatever you like to use) opened up and played the video for me.

Now, Google, don't you think it would be very non-evil of you to provide a player for Linux PPC yourself? =;)
