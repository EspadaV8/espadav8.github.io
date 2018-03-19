---
title: 'Django... One, no wait, two more things'
date: 2011-09-16 00:00:00 
tags: 
layout: post
---
Django has a load of admin files that need to be accessible. Rather than have the folder accessible as a standard folder I wanted to use a symlink inside the public_html folder. With the default Arch `mod_userdir` settings though, symlinks aren't followed unless the dir is owned by the user. This won't work though so a change to the Options is needed

```
Options FollowSymLinks
```

That needs to exist instead of the `SymLinksIfOwnerMatch` option.

---

The other thing is the fcgi file. By default you won't be able to run it within the public_html folder. To fix this add `ExecCGI` to the options section as well.


