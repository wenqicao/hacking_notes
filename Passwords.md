# PASSWORD ATTACKS

Hash Formats
------------

* MD5: 32-digit hexadecimal number


Cracking
--------

Cracking MD5 with John the Ripper:

`john --format=raw-MD5 md5.txt`

where md5.txt contains the hash in this format: Bob:1c0b76fce779f78f51be339c49445c49  

* [John the Ripper Hash Formats](http://pentestmonkey.net/cheat-sheet/john-the-ripper-hash-formats)  

Online MD5 cracker: [HashKiller](https://hashkiller.co.uk/md5-decrypter.aspx)

Ophcrack is a Windows Password cracker based on Rainbow Tables.  
http://blog.gdssecurity.com/labs/2010/9/14/automated-padding-oracle-attacks-with-padbuster.html  
PADDING ORACLE attack   
https://www.owasp.org/index.php/Testing_for_Padding_Oracle_%28OTG-CRYPST-002%29  


Bruteforcing
------------

* [Bruteforcing Web Form With Hydra](http://null-byte.wonderhowto.com/how-to/hack-like-pro-crack-online-web-form-passwords-with-thc-hydra-burp-suite-0160643/)


Wordlists
---------

* [Dictionaries + Wordlists](https://blog.g0tmi1k.com/2011/06/dictionaries-wordlists/) - how to customize wordlists
* [CIRT](https://cirt.net/passwords) - default password DB
* [Weakpass](http://weakpass.com/lists) - various password lists
* [SkullSecurity](https://wiki.skullsecurity.org/Passwords) - various password lists
* [Hashes.org](https://hashes.org/public.php) - shared community password recovery


Other Resources
---------------

* https://md5hashing.net/hash_type_checker  
