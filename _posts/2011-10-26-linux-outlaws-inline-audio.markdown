---
title: 'Linux Outlaws inline audio'
date: 2011-10-26 00:00:00 
tags: 
layout: post
---
Possibly the best Linux podcast, [Linux Outlaws](http://sixgun.org/linuxoutlaws), have show notes for each episode they release and on those pages they have downloads for the mp3 and ogg files. However, I like listening to them in the browser so I cobbled together a little bit of JavaScript to add an HTML5 audio tag before the download links.

<a href="javascript:(function()%20%7Bvar%20mp3%20%3D%20jQuery('.field-name-field-mp3%20a').attr('href')%3Bvar%20ogg%20%3D%20jQuery('.field-name-field-ogg%20a').attr('href')%3BjQuery('.field-name-field-ogg').remove()%3BjQuery('.field-name-field-mp3').empty().html('%3Cdiv%20class%3D%22field-item%20even%22%3E%3Caudio%20autobuffer%3D%22autobuffer%22%20preload%3D%22auto%22%20controls%3D%22controls%22%20tabindex%3D%220%22%3E%3Csource%20src%3D%22'%2Bogg%2B'%22%20%2F%3E%3Csource%20src%3D%22'%2Bmp3%2B'%22%20%2F%3E%3C%2Faudio%3E%3Cbr%20%2F%3E%3Ca%20href%3D%22'%2Bogg%2B'%22%3EOgg%20Vorbis%20Audio%3C%2Fa%3E%3Cbr%20%2F%3E%3Ca%20href%3D%22'%2Bmp3%2B'%22%3EMP3%20Audio%3C%2Fa%3E%3C%2Fdiv%3E')%3B%7D)()%3B">Drag me to your bookmarks bar</a> an on a show notes page, click it. You should see an audio player with controls appear just before the download links.
