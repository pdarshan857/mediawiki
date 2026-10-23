# MediaWiki Server on Ubuntu

By Darshan Patel

This is my MediaWiki project for WEB-401 (IaaS Deployment) at St. Clair College. I set up a wiki server on an Ubuntu VM in VirtualBox and showed it to my professor in a live demo.

## What I used

- Ubuntu Server (VirtualBox VM)
- Apache
- MariaDB
- MediaWiki (runs at /wiki)

## Files in this repo

- apache/000-default.conf - Apache config
- mediawiki/LocalSettings.php - MediaWiki settings (I took out the passwords and keys)
- netplan/00-installer-config.yaml - network config for the VM

## Private wiki

I set the wiki so people who aren't logged in can't read it, edit it, or make an account:

```php
$wgGroupPermissions["*"]["createaccount"] = false;
$wgGroupPermissions["*"]["edit"] = false;
$wgGroupPermissions["*"]["read"] = false;
```

## Issue during the demo

Everything worked fine when I built it at home. When I went to show it to my professor at college, the wiki wouldn't load.

It took me around 30 minutes to figure out. The VM was using DHCP, so on the college network it got a different IP. But $wgServer in LocalSettings.php still had my old IP in it. I changed $wgServer to the new IP and it worked again.

Next time I'd either set a static IP or let MediaWiki pick up the address by itself:

```php
$wgServer = "http://" . $_SERVER['HTTP_HOST'];
```

## Note

Passwords, keys and IP addresses in these files are replaced with placeholders.
