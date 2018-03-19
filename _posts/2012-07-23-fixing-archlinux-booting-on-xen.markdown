---
title: 'Fixing ArchLinux booting on Xen'
date: 2012-07-23 00:00:00 
tags: 
layout: post
---
I recently updated the kernel my VPS was running and it resulted in an unbootable system.

From the recovery console

```
modprobe xen-blkfront
```

You should then be able to see `/dev/xvda1`. You can mount this to read the data off your partition

```
mkdir tmp-root
mount /dev/xvda1 /tmp-root
```

In my case I needed to edit the `/etc/rc.conf` file and add the following to the MODULES section

```
xen-platform-pci xen_netfront xen-blkfront xen-pcifront xenfs
```

Save the file and reboot and exit out of the recovery console and it'll hopefully continue to boot.

After this things seem to be working ok, but I'm unable to reboot the server without having to login to the console and modprobe xen-blkfront again. Simply doing that 1 thing and ten exiting the recovery console allows the system to boot again. I'm assuming that there's a kernel module that I need to compile in somewhere but am unsure where exactly.
