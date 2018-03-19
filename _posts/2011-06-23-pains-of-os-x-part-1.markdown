---
title: 'Pains of OS X - Part 1'
date: 2011-06-23 00:00:00 
tags: 
layout: post
---
This was originally meant to be a series of problems that I've noticed with OS X when the office switched to it from Windows XP.

There have been so many problems and things wrong with it that I initially wanted to start doing a daily post with something new I found, however, I never got around to it and most of the problems I now have workarounds for.

This first post now though is more to do with Samba (I think) than OS X.

Working on a remote server at the office has both advantages and disadvantages. It means that there's only 1 server with everyone work on to back up. Since it's all in the same place, you can simply 'cd' into someone else work and help them fix a bug.

The main disadvantage though is the speed. Everything is on a remote server, and even over a local network there's a delay in saving, editing, etc. This has reared its ugly head lately as I've been trying to use git as DVCS.

One of gits plus points is that it's fast. And in this case, it's too fast. Connecting to the server via Samba (cifs://… in OS X) and trying to run pretty much anything other than git diff and git commit throw an error of one sort or another.

Git problem? Possibly.
Samba issue? Maybe.
Slow network? Who knows.

Whatever it was, it's a problem. I was able to use it to create the repo locally, rsync the files over to the remote folder, and then sync them back and forth whenever something needing committing and pushing. This wasn't very nice, so I started looking for something that does this automatically. I was pointed to autosync4mac by a friend, and even tried to hack it to support bi-directional syncing, but in the end, this it just a band-aid to the real problem. Mounting over SMB isn't working.

Last night I had an epiphany. Something in KDE, called KIO, allows you to mount pretty much anything as a folder. Websites, FTP connections and also SSH connections. Hmm, I said, I wonder if OS X has something similar based on FUSE . After a bit of searching I found MacFUSE and SSHFS, however, they are pretty dated now, but I installed SSHFS via MacPorts and started playing around. After I while I ended up with this…

`sshfs -o idmap=user -o uid=<osx-user-id> -o gid=<osx-group-id> -o allow_other <username>@<host>:<path> ~/Workspace/<host>`


The user id (uid) and group id (gid) I found from

`$ id <username>`

I picked the first group that made sense to me (admin). I mounted it in ~/Workspace/ since that's where most of the work that I do ends up, and it means that it's not creating mess in the /Volumes folder. You should be able to mount it wherever you like.

It's not ideal. It would be nice if there was a way to stick with the SMB approach, but that doesn't seem to be an option in this case.

What are the pains in all of this? The difficulty of getting anything outside of Apples walled garden to work. Installing MacFUSE and SSHFS was painful (there are many different attempts tried using their installs and some self compiling). There are a number of GUIs out there for handling this, but the lack features and in some cases aren't supported past 10.5.


