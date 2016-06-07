# METASPLOIT

* [Metasploit Unleashed](https://www.offensive-security.com/metasploit-unleashed/) - the ultimate guide to the Metasploit Framework

Starting
--------
```
service postgresql start
msfdb init
msfconsole
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
