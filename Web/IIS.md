# IIS (MICROSOFT INTERNET INFORMATION SERVICES) EXPLOITING

General info:

* https://www.alertlogic.com/blog/internet-information-server-%28iis%29-exploitation/  
* https://www.exploit-db.com/exploits/19033/  
* https://www.alertlogic.com/blog/internet-information-server-(iis)-exploitation/

Shortname Enumeration
=====================

Useful tool: https://github.com/irsdl/iis-shortname-scanner/  

Other tools/info:

https://webbreacher.wordpress.com/2014/10/23/tilde-enumeration/
http://www.acunetix.com/blog/web-security-zone/windows-short-8-3-filenames-web-security-problem/

https://soroush.secproject.com/blog/2012/06/microsoft-iis-tilde-character-vulnerabilityfeature-short-filefolder-name-disclosure/
https://www.youtube.com/watch?v=XOd90yCXOP4
http://stackoverflow.com/questions/11948857/iis-tilde-vulnerability-issue
http://www.slideshare.net/webbreacher/iis-tilde-enumeration-vulnerability

Admin Directory Bypass
======================

Example:  
```
http://127.0.0.1/backend/admin:$i30:$INDEX_ALLOCATION/admin.asp
```

Tip: don't forget to append the file name at the end.

Padding Oracle
==============

Look for webresource.axd.

* [Padding Oracle Attack Explained](http://www.securitylearn.net/tag/padbuster/)
