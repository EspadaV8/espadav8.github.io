---
title: 'PHP in_array recursive'
date: 2011-06-17 00:00:00 
tags: 
layout: post
---
I was just asked if I could think of an easy way to find if an item is in a multidimensional array, the quick solution I came up with was;

```php
$array = array('test', array('boo', 'foo', 'bar', array('baz')));
$exists = strpos('baz', json_encode($array));
```

This would fail for a few cases, if you had '1baz2' it'd also find it, and with named arrays it would also match keys as well. Both these are easy to work around though ('"baz"' or ':"baz"').

You could also use preg_match if you needed something a bit more advanced.
