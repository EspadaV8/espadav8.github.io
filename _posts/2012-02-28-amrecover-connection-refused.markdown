---
title: 'amrecover - Connection refused'
date: 2012-02-28 00:00:00 
tags: 
layout: post
---
I've been testing out amanda recently and got stuck when trying to test the `amrecover` program. I was constantly getting a 'connection refused' error and the following output in the debug log

```
1330398284.772118: amrecover: connect_portrange: Connect from 0.0.0.0.516 failed: Connection refused
1330398284.772130: amrecover: connect_portrange: connect to 172.16.2.134.10080 failed: Connection refused
1330398284.772145: amrecover: stream_client: Could not bind to port in range 512-1023.
```

The solution to this was to edit the server and change the `/etc/xinetd.conf/am*` files with the following settings

```
socket_type = stream
wait = no
protocol = tcp
```

Restart xinetd and you should be able to get further along. Now to find out why I'm getting an EOF error **sigh**
