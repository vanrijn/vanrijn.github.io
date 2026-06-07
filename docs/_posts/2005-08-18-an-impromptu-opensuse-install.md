---
layout: post
title: An impromptu OpenSuse install
date: 2005-08-18 23:29:40.000000000 -07:00
published: true
categories:
- Life in General
tags: []
permalink: "/2005/08/18/an-impromptu-opensuse-install/"
---

[![opensuse]({{site.baseurl}}/assets/2005/08/3068421304_f89c022b0b_o.gif)]({{site.baseurl}}/assets/2005/08/3068421304_f89c022b0b_o.gif "opensuse by vanRijn") I am not, by nature, someone who enjoys doing the same thing over and over and over again. Variety is most certainly the spice of life. This holds true in every aspect of my life. The Linux distributions that I use are no different. For the longest time, I used nothing but [Debian](http://debian.org/) unstable (like we're talking 4+ years here...). Then at some point I switched and started using [Fedora Core](http://web.archive.org/web/20171023090737/http://fedora.redhat.com/), and pretty much enjoyed it except for the annoyances regarding mp3 playback and other minor nits. In fact, I have 2 computers at home running Fedora Core 3 still.

Then, predictably, I got bored with it and wanted to see what the other Linux distributions had been up to, so I installed [Mandriva LE 2005](http://mandriva.com/) and have been running it very happily for the last several months. And don't get me wrong--the latest Mandriva (formerly Mandrake) is the best Mandrake release that I've seen yet! Very polished, very smooth and very well done. I don't think I had *any* complaints or problems with it. For the most part, everything worked pretty smoothly.

And then there's that one distribution that I have always loved for its stability and polish. [SuSE](http://suse.com/) is simply the best distribution around, IMHO, for a complete, stable desktop. The 2 problems that I have always had with it was that 1) they make you pay for their distribution, unless you want to wait a few months until they let you have it for free and 2) the packages that come with SuSE become quickly non-bleeding edge. This, obviously, is the tradeoff one makes for stability.

But just recently, Novell has done a very smart thing in sponsoring SuSE to open up its development cycle and allow the great unwashed to participate in enjoying its SuSE releases, going through the beta process and all. They have created the [OpenSuSE.org](http://opensuse.org/) website and subsequently released SuSE 10.0, beta1.

So today, out of excitement, boredom, and the ever-present desire to see the latest and greatest stuff, I downloaded the 4 cds required to install OpenSuSE and rebuilt my laptop to run it as its core Operating System. I have for several years kept all of my personal stuff on a different partition, so it's dead simple to install a different distro--just reinstall the root filesystem, have it bring my existing home partition into the new setup and Bob's your Uncle.

After having worked with it for the last few hours, I cannot praise OpenSuSE enough. It is quite simply the best Linux installation and running system that I have ever seen. The attention paid to detail from the opening splash screen on the install CD to the grub boot menu complete with slick countdown animations to the absolutely gorgeous bootsplash initialization process... everything looks and feels absolutely perfect. Very well done, guys!!

The only annoyance I have had whatsoever is in trying to get VMWare workstation to work with OpenSuSE 10.0-beta1. I was catching a nasty null pointer in vmware's kernel modules that looked like this:

> Unable to handle kernel NULL pointer dereference at virtual address 00000069 printing eip: c02a4eb9 *pde = 36f04001 Oops: 0000 [#1] SMP Modules linked in: vmnet(U) vmmon(U) nfs lockd md5 ipv6 parport_pc lp parport autofs4 sunrpc softdog dm_mod video button battery ac uhci_hcd ehci_hcd shpchp i2c_viapro i2c_core snd_via82xx gameport snd_ac97_codec snd_seq_dummy snd_seq_oss snd_seq_midi_event snd_seq snd_pcm_oss snd_mixer_oss snd_pcm snd_timer snd_page_alloc snd_mpu401_uart snd_rawmidi snd_seq_device snd soundcore via_rhine mii floppy ext3 jbd sata_via libata sd_mod scsi_mod CPU: 1 EIP: 0060:[] Tainted: P VLI EFLAGS: 00010282 (2.6.11-1.1353_FC4smp) EIP is at sk_alloc+0x10/0x146 eax: 00000010 ebx: 00000220 ecx: 00000001 edx: 00000220 esi: f54d86dc edi: f54d86e1 ebp: f7a2d2c0 esp: f568ae08 ds: 007b es: 007b ss: 0068 Process vmnet-bridge (pid: 3544, threadinfo=f568a000 task=f7935020)

So, after beating my head against the wall for a few minutes, starting to downgrade gcc to 3.3.5 and the kernel to the latest stable version, I found [this thread](http://groups.google.com/group/vmware.for-linux.experimental/browse_thread/thread/dd2dcd20060ca441/47d35ce566854d2e?lnk=st&q=vmware+gcc-4&rnum=1&hl=en#47d35ce566854d2e) that looked to be the same as what I was seeing--and more importantly, found that the answer to the problem was to download the latest vmware-any-any-update* from [this wonderful website](http://ftp.cvut.cz/vmware/). And, fortunately, it seems to have done the trick. I'm using vmware now and it seems to be behaving itself. For the record, it seems that the problem is somewhere in the combination of the newer 2.6 Linux kernel, GCC-4, and vmware's module coding.

But other than that, I am seriously impressed with OpenSuSE. I heartily recommend it to both experienced Linux users and also those who are curious as to what this whole Linux craze is about. Job extremely well-done, guys. =:)
