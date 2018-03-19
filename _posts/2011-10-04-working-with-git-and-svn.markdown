---
title: 'Working with Git and SVN'
date: 2011-10-04 00:00:00 
tags: 
layout: post
---
I work in an environment where all the work needs to be done on a remote host with my working folder mounted over a Samba share. All the source is stored in an SVN repo. Ideally I'd like to be able to use Git but something with the samba share causes an error with `git svn clone` (not going to go into that now, but this is the error for reference).

```
git svn clone http://id-hub/master/clients/client/test/publish/trunk test-project.git
Initialized empty Git repository in /Volumes/samba-share/dev/asmith/client/test.git/.git/
W: Ignoring error from SVN, path probably does not exist: (160013): Filesystem has no item: '/master/!svn/bc/100/clients/client/test/publish/trunk' path not found
W: Do not be alarmed at the above message git-svn is just searching aggressively for old history.
This may take a while on large repositories
r12208 = a61f1d1b6bc8b267fb2d247878697a4953e87e39 (refs/remotes/git-svn)
fatal: Cannot open '.git/2IlhwN8uea': Resource temporarily unavailable
hash-object -w --stdin-paths --no-filters: command returned error: 128
error closing pipe: Bad file descriptor at /usr/local/Cellar/git/1.7.7/libexec/git-core/git-svn line 0
error closing pipe: Bad file descriptor at /usr/local/Cellar/git/1.7.7/libexec/git-core/git-svn line 0
```

What I end up doing is working in an SVN checkout on the share and create a Git clone locally. Do some work on the SVN version and then copy all the changes over to the Git clone so that I can do partial commits and whatnot and then svn dcommit back. The problem lies with syncing things back to the Git clone.

I've tried using rsync but for some reason or another it wants to copy everything all the time which is slow. Instead, I created this little one liner to check for changes and copy them over instead. It could probably be tidied up but it works well enough for me

```
$ pwd
/path/to/svn/checkout
$ while read line
while> do cp -v "$line" /path/to/git/clone/"$line"
while> done < <(svn status --ignore-externals |grep -e '^[MDRA!?]'|awk {'print $2,$NF'})
```

All it does is check the status of the svn checkout (ignoring externals) and grep the list so that only changes are shown. It then splits that with awk from the second field to the end (for folders/files with spaces in them). This list is then passed to the while loop where each line is read in and a copy from the current location to the git clone is performed.

This probably isn't useful to anyone so this is mostly just a post as a reminder for me.
