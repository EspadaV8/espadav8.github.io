---
title: 'Rooting the S2'
date: 2011-10-12 00:00:00 
tags: 
layout: post
---
I recently got myself the new-ish Samsung Galaxy S2 android phone. My first android phone and I'm really happy with it. With the release of CyangonMod 7.1 the other day though I wanted to have a go at rooting the phone and installing custom ROMs.

While reading up on things though I started confusing myself. The wiki for CM mentions things like ClockworkMod Recovery, ROM Manager and rooting. A backup tool they mention, Titanium Backup, needs root to work.

This is just a note of what I've gone through to get part of the way through.

The first thing that you need to do is get a custom, 'insecure', kernel installed. This comes in the form of [codeworkx ClockworkMod Recovery](http://forum.xda-developers.com/showthread.php?t=1118693).

I flashed this first using Odin. It took about 30 seconds at most.

After that had completed the phone reboots with a yellow triangle. Next up is getting root access. This is needed if you just want to flash CM7.1. However, I wanted to check out Titanium Backup and ROM Manager that both need root access.

The usual way of doing this is via [SuperOneClick](http://forum.xda-developers.com/showthread.php?t=803682) but that kept crashing at step 6, so I used [S2 Root](http://forum.xda-developers.com/showthread.php?t=1125414) instead and that worked first time.

That was it. The phone is now rooted. I've not yet checked ROM Manager or CM7.1, that’s to come after Titanium Backup.
