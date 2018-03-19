---
title: 'Gitlab - Mirror pushing to GitHub'
date: 2016-08-23 00:00:00 
tags: 
layout: post
---
I'm in the process of moving some personal projects from [GitHub](https://github.com) to the hosted version of [GitLab](https://gitlab.com) (for a number of reasons, an important one being that GitLab have a nice large [Open Core](https://en.wikipedia.org/wiki/Open_core) code base).

As part of this though I'd like GitHub repos to keep working so I wanted to set up mirroring of the repo on GitLab to GitHub. Support is including in GitLab and set up is fairly straight for public repos, just provide the URL of the mirror (`http`, `https` or `git` URL). However, with GitHub the repos require authentication to push changes. You can normally provide these details in the URL itself, e.g. `https://EspadaV8:password@github.com/EspadaV8/Picfinity.git` but when 2FA is enabled on the account you're not able to do this. Instead you need to generate a [new access token for GitLab](https://github.com/settings/tokens/new?scopes=repo&description=GitLab+mirror) to use as a password. I've tested with the `repo` permission and mirroring works but you may be able to reduce the permission set.

Once you have a token just update the mirror URL and include that as the password, e.g. `https://EspadaV8:13bc40ba0f3344e2b0f089ee0e4f756f534974ab@github.com/EspadaV8/Picfinity.git` (that token has been deleted and won't work).

Simple.
