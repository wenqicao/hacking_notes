# WINDOWS

* [PowerSploit](https://github.com/PowerShellMafia/PowerSploit) - collection of powershell modules for pentesting
* [Nishang](https://github.com/samratashok/nishang) - Powershell framework and collection of scripts and payloads for pentesting 
* [USBDumper](http://www.secuobs.com/USBDumper.rar) - silently copies contents of every connected USB device to the system
* [mimikatz](https://github.com/gentilkiwi/mimikatz) - extract plaintext passwords, hashes, PIN codes, kerberos tickets from memory; pass-the-hash
* [CrackMapExec](https://github.com/byt3bl33d3r/CrackMapExec) - a swiss army knife for pentesting Windows/Active Directory environments

Privilege Escalation
--------------------

* [Windows Privilege Escalation Fundamentals](http://www.fuzzysecurity.com/tutorials/16.html)
* [AccessEnum](https://technet.microsoft.com/en-us/sysinternals/bb897332.aspx) - tool for analyzing files/dirs user rights
* [Autoruns](http://technet.microsoft.com/en-us/sysinternals/bb963902.aspx ) - tool for managing autorun apps
* [AccessChk](https://technet.microsoft.com/en-us/sysinternals/bb664922.aspx)
* [PowerUp](https://github.com/PowerShellMafia/PowerSploit/tree/master/Privesc) - clearinghouse of common Windows privesc vectors that rely on misconfigurations

Post-Exploitation
-----------------

* [Post-Exploitation with "Incognito"](http://hardsec.net/post-exploitation-with-incognito/?lang=en)


Null Session
------------

Open ports? UDP 137 & 138, TCP 139  
`net use \\host\IPC$ "" "/user:"`
