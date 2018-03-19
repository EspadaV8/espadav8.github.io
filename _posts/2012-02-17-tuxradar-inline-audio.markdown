---
title: 'TuxRadar inline audio'
date: 2012-02-17 00:00:00 
tags: 
layout: post
---
Similar to the [Linux Outlaws](http://sixgun.org/linuxoutlaws) inline audio bookmarklet I’ve created one for [TuxRadar](http://www.tuxradar.com/) as well

<a href="javascript:(function()%7Bfunction%20getScript(url%2Csuccess)%7B%20var%20script%3Ddocument.createElement('script')%3B%20script.src%3Durl%3B%20var%20head%3Ddocument.getElementsByTagName('head')%5B0%5D%2Cdone%3Dfalse%3Bscript.onload%3Dscript.onreadystatechange%3Dfunction()%7Bif(!done%26%26(!this.readyState%7C%7Cthis.readyState%3D%3D'loaded'%7C%7Cthis.readyState%3D%3D'complete'))%7Bdone%3Dtrue%3Bsuccess()%3Bscript.onload%3Dscript.onreadystatechange%3Dnull%3Bhead.removeChild(script)%3B%7D%7D%3Bhead.appendChild(script)%3B%7DgetScript('%2F%2Fajax.googleapis.com%2Fajax%2Flibs%2Fjquery%2F1.7.1%2Fjquery.min.js'%2Cfunction()%7Bif(typeof%20jQuery%3D%3D'undefined')%7Balert('There%20was%20an%20error%20loading%20the%20jQuery%20JS%20file.%20Sorry.')%3B%7Delse%7B%24jq%3DjQuery.noConflict()%3Bvar%20l%3D%24jq('.podcastdownload')%3Bvar%20ogg%3Dl.find('a%5Bhref%24%3D%22ogg%22%5D')%3Bvar%20mp3%3Dl.find('a%5Bhref%24%3D%22mp3%22%5D')%3Bl.empty().html('%3Cdiv%20style%3D%22margin%3A0%200%2015px%200%3B%22%3E%3Caudio%20autobuffer%3D%22autobuffer%22%20preload%3D%22auto%22%20controls%3D%22controls%22%20tabindex%3D%220%22%3E%3Csource%20src%3D%22'%2Bogg.attr('href')%2B'%22%20%2F%3E%3Csource%20src%3D%22'%2Bmp3.attr('href')%2B'%22%20%2F%3E%3C%2Faudio%3E%3C%2Fdiv%3E%3Cp%3E%3Cstrong%3E%3Ca%20href%3D%22'%2Bogg%2B'%22%3E'%2Bogg.text()%2B'%3C%2Fa%3E%3C%2Fp%3E%3Cp%3E%3Ca%20href%3D%22'%2Bmp3%2B'%22%3E'%2Bmp3.text()%2B'%3C%2Fa%3E%3C%2Fstrong%3E%3C%2Fdiv%3E')%3B%7D%7D)%3B%7D)()%3B">TuxRadar inline audio</a> Drag that link to your bookmarks bar and click when you’re on a Podcast page on [TuxRadar](http://www.tuxradar.com/).

Full source is available on GitHub – https://gist.github.com/1848992
