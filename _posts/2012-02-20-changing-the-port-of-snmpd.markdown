---
title: 'Changing the port of SNMPD'
date: 2012-02-20 00:00:00 
tags: 
layout: post
---
Took me a while to figure this out but it’s simple to do. In snmpd.conf add the following

```
agentaddress 0.0.0.0:8080
```

This will make snmpd listen on all interfaces on port 8080. 8080 can be changed to whatever port you feel like (so long as something else isn’t using it).


