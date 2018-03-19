---
title: 'Squeaky audio with WinUAE'
date: 2014-09-27 00:00:00 
tags: 
layout: post
---
After firing up WinUAE after a while and loading in an old Legend save I noticed that the audio would squeak/distort every few seconds. After trying a number of suggestions from places with nothing making any difference (sound buffer size, interpolation, audio filter, sound driver, along with a number of display settings) I noticed an option under `CPU and FPU` titled `CPU Emulation Speed`. Default setting was `Fastest possible`, toggling this to `Approcimate A500/A1200 or cycle-exact` fixed the audio problems and also dropped CPU usage from being pegged at 100% to <10%.
