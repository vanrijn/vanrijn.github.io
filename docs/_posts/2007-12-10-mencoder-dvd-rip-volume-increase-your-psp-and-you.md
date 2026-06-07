---
layout: post
title: Mencoder, DVD Rip, Volume Increase, Your PSP, and You!
date: 2007-12-10 02:27:32.000000000 -08:00
published: true
categories:
- Linux
tags: []
permalink: "/2007/12/10/mencoder-dvd-rip-volume-increase-your-psp-and-you/"
---

Holy crap. The time between iterations of testing video encoding is prohibitive to quick progress as well as a (several) good night's sleep.

After much pain and gnashing of teeth, I present you with the result of the last 3 hours of my life.

> time nice mencoder dvd://1 -sws 9 \ -aid 128 -af volume=15:0 \ -vf pullup,softskip,dsize=480:272,scale=0:0,harddup,unsharp=l3x3:0.7 \ -ofps 24000/1001 \ -oac faac -faacopts br=128:mpeg=4:object=2:raw -channels 2 -srate 48000 \ -ovc x264 -x264encopts bitrate=500:global_header:partitions=all:trellis=1:level_idc=30 \ -of lavf -lavfopts format=psp -info name="Tomb Raider" -o "$HOME/Movies/TombRaider.mp4"

Sincere thanks to [forgeflow's answer to this ubuntu forum post](http://ubuntuforums.org/showthread.php?t=525675) and to his excellent [videogeek site](http://videogeek.shacknet.nu/index.php?entry=entry070917-130603).

Other observations:

- There is far more complexity to audio/video encoding than I'd ever want to understand fully.
- Anyone who actually understands mencoder fully deserves to be the next US president.
- No, seriously, I'd vote for him/her.
- The above incantation of mencoder accomplishes what I need it to, namely:
  - Rips a full DVD for me without having to pull it into an intermediary file.
- Increases the volume of the ripped/encoded track by 20 decibels in this case.  Handbrake doesn't yet let you do that.
- Takes advantage of the newer PSP System Software's ability to handle H264 encoding (which I hear is what all the cool kids are using these days).
- This same thing (without being able to turn the volume up) is possible in Handbrake with this:
> ~/local/HandBrakeCLI -i /dev/dvd --longest --size 800MB -e x264 -x ref=2:mixed-refs=1:bframes=3:b-rdo=1:bime=1:weightb=1:subme=6:trellis=1:analyse=all:level=3:no-fast-pskip:me=umh --crop 0:0:0:0 -R 48 -b 1024 -w 480 -l 272 --markers -o ~/Movies/TombRaider.mp4
- Yes, I am not ashamed to admit it: I like Tomb Raider.  Angelina and I were married in an alternate dimension, and I can beat Tomb Raider Legends in 2 hours with my eyes closed.
- One or more of the statements made in the above bullet point may be more the result of sleep-deprivation than actual truth.

Good night, Gracie.

**[ Update ] ** Okay, nuts... apparently this video quality isn't quite good enough because now I'm seeing weird ghosting on the PSP while watching the resultant movie. Yay, another geekly late night tonight....

**[ Update 2008-03-04 ]** I've updated the command that I'm using now with mencoder, thanks to some comments and tweaks during the past few months.
