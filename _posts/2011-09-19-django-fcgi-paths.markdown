---
title: 'Django - fcgi paths'
date: 2011-09-19 00:00:00 
tags: 
layout: post
---
As mentioned before, I've had problems setting up Django with the fcgi script. Today I came across another problem.

While going through the tutorial it walks you through the process of enabling the built in admin module. When I did this as added my module to settings.py file I got an error along the lines of

```
Unhandled Exception
An unhandled exception was thrown by the application.
```

Not very helpful by itself, but tracking it down in the Apache logs it came down to it being unable to find a module that had been added to the settings file (in the tutorial it’s the `polls` app that you create).

My fix for this was to add the project path to the python path in the fcgi script. In my previous post I said that the fifth line needed to point to the folder above your project folder. This works so that you can load the settings file but fails for any other module/model that you want later. Instead, line 6 should be the folder above your project and line 5 should be your project folder, i.e.

```python
sys.path.insert(0, "/home/espadav8/Workspace/mysite")
sys.path.insert(0, "/home/espadav8/Workspace")
```

The other fix seems a bit less elegant is to change any instance of `polls` into `mysite.polls`.


