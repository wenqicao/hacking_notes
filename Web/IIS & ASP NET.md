# IIS (MICROSOFT INTERNET INFORMATION SERVICES) / ASP.NET EXPLOITING

General info:

* https://www.alertlogic.com/blog/internet-information-server-%28iis%29-exploitation/  
* https://www.exploit-db.com/exploits/19033/  
* https://www.alertlogic.com/blog/internet-information-server-(iis)-exploitation/

Shortname Enumeration
=====================

Useful tool: https://github.com/irsdl/iis-shortname-scanner/  

Other tools/info:

* https://webbreacher.wordpress.com/2014/10/23/tilde-enumeration/
* http://www.acunetix.com/blog/web-security-zone/windows-short-8-3-filenames-web-security-problem/
* https://soroush.secproject.com/blog/2012/06/microsoft-iis-tilde-character-vulnerabilityfeature-short-filefolder-name-disclosure/
* https://www.youtube.com/watch?v=XOd90yCXOP4
* http://stackoverflow.com/questions/11948857/iis-tilde-vulnerability-issue
* http://www.slideshare.net/webbreacher/iis-tilde-enumeration-vulnerability

Admin Directory Bypass
======================

Example:  
```
http://127.0.0.1/backend/admin:$i30:$INDEX_ALLOCATION/admin.asp
```

Tip: don't forget to append the file name at the end.

Padding Oracle
==============

Look for `WebResource.axd` (access the static resources embedded in the application assemblies) or `ScriptResource.axd` (access to JavaScripts embedded in the assemblies or stored on the disk).

* [Padding Oracle Attack Explained](http://www.securitylearn.net/tag/padbuster/)
* [ASP.NET Padding Oracle File Download (MS10-070)](https://www.exploit-db.com/exploits/15265/)


ASP.NET
-------

Determine if stack traces are enabled: `host.com/default|.aspx`  
Invalidate .NET Monitoring with a virtual directory identifier: `host.com/default~.aspx`  
Detailed application level trace information (rarely enabled): `host.com/trace.axd`   
Most important file: web.config (located inside the document root).  
`__VIEWSTATE` variable contains application state (applicaton variables and control attributes). Viewstate contents can be decoded using a [ViewState Decoder](http://www.pluralsight.com/tools.aspx).  
[Drop and Pop](http://ha.cked.net/dropandpop.zip) - .NET reverse shell dropper  
