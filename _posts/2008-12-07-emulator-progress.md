---
layout: post
title:  "Emulators made progress"
date:   2008-12-07
tags: emulator
---
Lots of applications become legacy after old hardware stopped manufacturing, and emulators emerged and became the savior. VMware, VirtualPC, VirtualBox, QEMU and Xen emulate a i386 PC. VirtuaNES, VisualBoyAdvance, Gens, Snes9x, Project1964 … emulate different game platforms.

Recent version of PCSX2 enables user to run PS II games at almost full speed provided he has the game DVD, a good enough CPU (better than Intel Core 2 Duo E6600), and at least 2 GiB memory. Of course, correct plug-ins should be configured in order to run a game smoothly. And you have to get the bios files to run the application correctly. The mod versions run better than the official binary, thanks to its opened source.

DOSBox implemented basic support for 32-bit protected mode DOS application 5 years ago. But it did not fully work for most applications until the recent version 0.72. Now "Case of the Rose Tattoo" can run fluently in DOSBox.

![img]({{ '/assets/images/Holmes2.jpg' | relative_url }}){: .center-image }*Holmes2*

The player has to enter some commands, or write them in [autoexec] section of a conf file for each game. The comprehensive conf file even supports filters such as hq2x, 2xsai, tv2x and supereagle, etc. Just like the game emulators did. Yes, those time-honored DOS applications revived :D
