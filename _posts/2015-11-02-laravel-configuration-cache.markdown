---
title: 'Clear Laravel configuration cache'
date: 2015-11-02 00:00:00 
tags: 
layout: post
---
You can cache the configuration files in Laravel using

```
php artisan config:cache
```

There's also a way to clear the cache

```
php artisan cache:clear
```

But, this won't clear the configuration cache. To do that you need to use

```
php artisan config:clear
```
