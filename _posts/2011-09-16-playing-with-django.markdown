---
title: 'Playing with Django'
date: 2011-09-16 00:00:00 
tags: 
layout: post
---
I've been playing around with [Django](https://www.djangoproject.com/) over the last few days and been having a few problems with it. I'll try to list them out here and what I've been able to do to get it working nicely.

A bit of a preface. I have a VPS running Arch Linux. I have Django 1.3 installed from the repos. The server is running Apache 2.2 and `mod_userdir` is installed and setup with the defaults. Django is being served by `mod_fastcgi`.

I've choosen mod_fastcgi since I'm also using this as a chance to see if Django is something that could possibly be used where I work and this setup better matches the server setup that's used there.

## The first problem with this is with the htaccess file.

```
AddHandler fastcgi-script .fcgi
RewriteEngine On
RewriteBase /~espadav8/
RewriteCond %{REQUEST_FILENAME} !-f
RewriteRule ^(.*)$ mysite.fcgi [QSA,L]
```

The special line there is the RewriteBase. Without it set to that you'll be met with errors of 'Object Not Found'. The 'espadav8' in that line should be replaced with your username for the system.

## After that you'll likely get errors in the .fcgi file.

```python
#!/usr/bin/python2
import sys, os
# Add a custom Python path.
sys.path.insert(0, "/home/espadav8/Workspace")
# Switch to the directory of your project. (Optional.)
os.chdir("/home/espadav8/Workspace/mysite")
# Set the DJANGO_SETTINGS_MODULE environment variable.
os.environ['DJANGO_SETTINGS_MODULE'] = "mysite.settings"
from django.core.servers.fastcgi import runfastcgi
runfastcgi(method="threaded", daemonize="false")
```

The pages that I've found that talk about this file make it a bit unclear as to which paths should be used. I assumed initially that both paths should be the same and that it should be the path to the project (i.e. /home/espadav8/Workspace/mysite). However, that doesn't work and you'll get an error about being unable to find 'mysite.settings'. The fix for this is to change the custom Python path to remove the 'mysite' part and use the folder above instead.

## Next up is URLs.

This is one I haven't found a nice solution for yet.

Because your access URL is something like

http://www.example.com/~espadav8/

You need the RewriteBase set as /~espadav8/ so that the 'correct' details are passed through Apache and the fcgi script can be loaded. However, this causes a problem when Django gets the URL since what you'd want to be the 'base' is actually /~espadav8/. In your urls.py file you then need to prefix everything with /~espadav8/. Initially this might not be an issue, but if you want to move the project around all of those would need to be updated.

Ideally it would be possible to define a setting file in INI format that would check the server and path setup and set a base_url or something similar so that projects could be moved freely and added in an ad-hoc way. Alas, this doesn't seem to be something that Django supports by default.
