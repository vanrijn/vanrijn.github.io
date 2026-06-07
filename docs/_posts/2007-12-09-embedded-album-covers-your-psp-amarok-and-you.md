---
layout: post
title: Embedded Album Covers, Your PSP, Amarok, and You
date: 2007-12-09 04:29:51.000000000 -08:00
published: true
categories:
- Linux
tags: []
permalink: "/2007/12/09/embedded-album-covers-your-psp-amarok-and-you/"
---

[![Amarok?]({{site.baseurl}}/assets/2007/12/2097398338_dd86ebe6bd_m.jpg)]({{site.baseurl}}/assets/2007/12/2097398338_dd86ebe6bd_m.jpg "Amarok? by vanRijn")So... first off, I Googled for Amarok, hoping to find some new sweet pixels and instead I find this. Um... ***so*** not the Amarok that I know and love.

Anyway, a couple of years ago, I won a PSP from the LinuxWorld convention. Being that I'm a geek, it was love at first boot jingle. Being that I am married, have 3 kids, work full-time++, and try to hack every once in a while, the brave little PSP spent a lot of alone time. Oh sure, I own several PSP games (go SOCOM2!!), but that's about it.

Until now.

Since I'm lucky enough to be able to work from home for a bit, I'm not driving back and forth to work every day and as such, I gave my iPod to my darling daughter. So I bought a 4G memory stick (oh, that reminds me, I need to blog about [stupid, evil, skanky eBay sellers of fraudulent flash memory, since I wasted my time with one personally...](http://www.flickr.com/photos/vr/2087255269/)) (but for non-fraudulent and kick-butt flash, I highly recommend [SanDisk's Gaming Pro Duo](http://www.nextag.com/Sandisk-Gaming-flash-memory-508602756/prices-html)... it's uber fast) (and that's enough parenthetical statements for one sentence). And, having this nice little PSP and 4G of disk space on it now, I've been figuring out how to put stuff of interest onto it.

Movies: Totally cool. The PSP has a 480x272 screen. Handbrake does a really nice job of ripping a DVD and creating an mp4 that the PSP can play perfectly. Really, really nice. Oooh, and the new PSP OS has this nifty little auto-generating movie browser thingey that is kind of like a scene selector on a DVD movie... lets you see scene selections for the movie at configurable intervals too... Anyway, the only beef I have with Handbrake thus far is that it doesn't allow me to increase the volume on the ripped movie. So I'm looking at ffmpeg now to see if it does as good a job as Handbrake. I'm sure I'll blog more about that later.

Music: Really cool here too. The PSP plays a variety of audio formats and has some really nice eye candy/visualizations/etc. for your music-listening pleasure. However (and this is what actually what prompted this post), it shows album covers per song only if they're embedded as APIC frames in your mp3's ID3 tag. Now, I'm new to this, and didn't know that there were such animals as APIC frames until just yesterday, but I did know that I wanted to put my album art into my little mp3s so that they'd show up all purty-like on my PSP (there, full circle now).

So, I've put in the usual geekly late night or two (yes, dear, I'm honestly coming to bed... in a sec...) and learned much about ID3 tags and the various tools that one might employ in one's attempt to embed album covers in one's mp3s. I even bugged [my good friend Seb](http://sebruiz.net/), who pointed me to a really cool ["EmbedCover" script](http://www.kde-apps.org/content/show.php/EmbedCover?content=32262) for amarok that I didn't know existed. But, along the learning curve, I saw a lot of complaints about Amarok showing distorted embedded album covers. My problem was slightly different in that I couldn't figure out how to get them embedded in the first place, let alone getting them there and then finding them distorted. Through trial and error (and aforementioned geekly late nights), I think I've found a consistent way to get album covers to be embedded and why they might show up distorted in Amarok (and other players too, mind you--it's not Amarok's fault).

The first step in getting album cover art embedded in my mp3s was to get a picture into each directory of my music. I organize things like this: "Artist - Album/Artist - Title.mp3", and in each folder, I want an album cover file. One way to do this is an amarok script called [CopyCover](http://www.kde-apps.org/content/show.php/CopyCover+%28amaroK+Script%29?content=22517). Assuming that you've first found all album art for your music via Amarok's cover manager, CopyCover will, as you are playing your music, copy the album art from Amarok's cache into the folder for your music and call it "cover.png". There's also an offline script that is supposed to do the job all at once instead of you having to do it the song-by-song way, but I couldn't get it to work for me... I think the database schema changed behind its back. An alternate route (and this is what I did) was to tell Amarok to organize all of my music for me (highlight all tracks in player and right-click, "Manage Files" | "Organize Files", and then click the "use cover art for folder icons" checkbox. Amarok will put a ".desktop" file in each of your folders and the "Icon" attribute will point to Amarok's cached album cover. I then wrote this simple function to copy this album art into the folder itself:

> function albumcoversfromamarok() { for f in * do count=$(ls --color=never $f | grep mp3| wc -l) echo "$count : $f" if [ $count -gt 0 ] then icon=$(cat "$f/.directory" 2>/dev/null | egrep "^Icon" | cut -d "=" -f2) [ -e "$icon" ] && cp "$icon" "$f/cover.png" fi done }

I then wrote 2 more simple functions that will rip through all of my folders and embed the updated album art into my mp3s:

> function mp3albumcoverdir() { if [ -e "cover.png" ] then convert -quality 90 -geometry 300x300\> cover.png cover.jpg else return fi for f in *.mp3 do echo "Embedding cover in: [$f]" mp3albumcover "$f" cover.jpg done }
>
>
> function mp3albumcover() { FILENAME="$1" IMAGE="$2"
>
>
> # first, remove existing images # do this for FRONT_COVER and OTHER APIC types and twice just to make sure we're clean eyeD3 --add-image=:OTHER "$FILENAME" >/dev/null 2>&1 eyeD3 --add-image=:OTHER "$FILENAME" >/dev/null 2>&1 eyeD3 --add-image=:FRONT_COVER "$FILENAME" >/dev/null 2>&1 eyeD3 --add-image=:FRONT_COVER "$FILENAME" >/dev/null 2>&1
>
>
> # now, get rid of cruft left behind by previous images id3v2 --APIC "" "$FILENAME" >/dev/null
>
>
> # make sure we have a valid id3 tag eyeD3 --to-v2.3 "$FILENAME" >/dev/null 2>&1 # now embed the image eyeD3 --add-image="$IMAGE":FRONT_COVER "$FILENAME" }

Then I run it from the top level of my music collection with "for f in *; do; mp3albumcoverdir "$f"; done".

Now, along the way, whenever I found an incorrect album cover embedded and tried to fix it by removing the previous album art and adding the new one, I started seeing the corrupted images in amarok that I'd been reading about. And it's not just that amarok wasn't able to read the images... they were truly corrupt. "eyeD3 --write-images=. $FILE" produced a corrupt image as well. And, every time I cleared the previous image and added a new one with eyeD3, I noticed that my filesize kept getting bigger and bigger. Even when I "removed" all images with eyeD3's "--add-image=:FRONT_COVER", the filesize of the mp3 just kept getting bigger. It was then that I tried setting the APIC frame to null ("") with id3v2, and that returned my mp3's filesize back to where it should be. And after that, if I added the album art to the mp3, it added it cleanly, my filesize looked sane again, and Amarok was able to see the embedded album art again.

So, my theory, [which is mine, and belongs to me and I own it, and what it is too](http://www.jumpstation.ca/recroom/comedy/python/elk.html), is that people who are seeing album art distortions/corruptions in amarok might possibly have files that either have more than one embedded picture, or have dirty APIC tags. If any of you, dear readers, is seeing embedded album art distortion in Amarok, would you please install id3v2 and eyeD3 onto your little Linux box and try running my mp3albumcover function against that mp3 with a new album image? I'd very much like to see if it fixes the problem for you.
