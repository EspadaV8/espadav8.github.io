---
title: 'cPanel and the woes of wildcard SSL'
date: 2011-03-24 00:00:00 
tags: 
layout: post
---
Here in the office we've recently needed to be able to have a number of subdomains that are accessible over HTTPS. The obvious solution to this is to install a wildcard SSL certificate and be done with it.

However, we use cPanel to manage accounts (where each subdomain would be a different account) and cPanel doesn't have any way to manage wildcard certificates. This causes problems. A quick Google search will show you a few attempts at how to fix this, but nothing seemed 'right' (neither does the solution below, but it seems nicer to me).

I'll first explain what I did and then go in to a bit more detail, for this I'll assume that you have the domain 'example.com' and a wildcard SSL certificate for '*.example.com'

1. Create an account as usual for your subdomain, e.g. store.example.com (username 'store')
2. Go to the SSL/TLS section and select 'Install a SSL Certificate and Setup the Domain'
3. In there you'll need to paste in the 'crt' and 'key' parts of the certificate and the optional 'ca bundle' if you have one
4. Domain – store.example.com
5. User – nobody
6. IP – The IP of your host (e.g. 192.0.32.10)
7. This will add an entry to the main http.conf file used by cPanel/Apache
8. Connect to your server over SSH and find the cPanel httpd.conf file (/usr/local/apache/conf/httpd.conf)
9. Edit this with your editor of choice and find the part that has the SSL site set up (it seems to appear near the end of the file)
10. Copy all this from the file and then delete it from there
11. Back in cPanel go to 'Main >> Service Configuration >> Apache Configuration >> Include Editor'
12. Select 'All Versions' from the 'Post VirtualHost Include' section and paste in the config details that you removed from the httpd.conf file
13. If you have suPHP enabled you need to change the 'nobody nobody' to 'store store'
14. Restart Apache
15. You should now be able to access https://store.example.com

What you basically end up doing is uploading the certificate via cPanel and letting it create the Apache vhost entry.

It has to be moved out of the main httpd.conf file because if you try and add in another site it'll complain that there's already a site set up on your IP address and that each site needs a unique IP, if it's not in the main file, cPanel doesn't care.

You might find that when you add a second subdomain that you can't access it, this is likely due to not having NameVirtualHosts set for port 443, you can enable this like so;

1. Go to 'Main >> Service Configuration >> Apache Configuration >> Include Editor'
2. Select 'All versions' for the 'Pre VirtualHost Include' and add the following

```
<IfDefine SSL>
NameVirtualHost *:443
</IfDefine>
```

This will enable name-based virtual hosts for port 443.
