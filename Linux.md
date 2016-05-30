# LINUX

General
-------

If ifconfig is not found, try this: /sbin/ifconfig

File permissions: owner:group:world x=1 w=2 r=4

Eliminating traces:

`iptables –flush; history -c; find ./ -name “*.log” |xargs rm`


User Management
---------------

* Add root user:

```
useradd -ou 0 -g 0 john
passwd john
```
* Switch user: `su`

* Change user password non-interactively: `echo "student:studying"|chpasswd`

* Add another non-root Kali user:

```
root@kali:~# useradd -m muts -G sudo -s /bin/bash
root@kali:~# passwd muts
Enter new UNIX password:
Retype new UNIX password:
passwd: password updated successfully
```

* Kill process: `kill -9 <pid>`  
* Force-delete user: `userdel -f <uid>`  

Networking
----------

Find open ports:
```
netstat --listen
lsof -i
```
Open ports and established TCP connections: `netstat -vatn`  
Only open UDP ports: `netstat -vaun`  
FQDN: `netstat -vat`  
Display all open IPv4 network files in use by the processes whose PID is 9255:
```
lsof -i 4 -a -p 9255
```

Privilege Escalation
--------------------

* [Basic Linux Privilege Escalation by g0tmi1k](https://blog.g0tmi1k.com/2011/08/basic-linux-privilege-escalation/)
* [Linux Exploit Suggester](https://github.com/PenturaLabs/Linux_Exploit_Suggester)
* [LinuxPrivChecker](http://www.securitysift.com/download/linuxprivchecker.py)
* [unix-privesc-check](http://pentestmonkey.net/tools/audit/unix-privesc-check)

Shell history:
```
cat ~/.bash_history
cat ~/.nano_history
cat ~/.mysql_history
```

Private SSH keys:
```
ls -la ~/.ssh/
cat ~/.ssh/id_rsa
cat ~/.ssh/id_dsa
```

Passwords in config files, backups:
```
find /etc/ -name "*.conf" -exec grep -i pass {} \;
find / -type d -name "*backup*"
find / -name "*backup*" | grep "\.tar\|\.gz\|\.zip\|\.bz2\|\.bak"

Shell
-----

`>` - redirects standard output of a command to a file, overwriting previous content  
`>>` - redirects standard output of a command to a file, appending new content to old content  
`<` - redirects standard input to a command  
`|` - redirects standard output of a command to another command  
`sort` - sorts lines of text alphabetically  
`uniq` - filters duplicate, adjacent lines of text  
`grep` - searches for a text pattern and outputs it  
`sed` - searches for a text pattern, modifies it, and outputs it  
`source ~/.bash_profile` - activate updated profile settings in current session  
`history` - view command history  
`export PS1=">> "` - change default prompt from $ to >>  
`env` - return environment variables  
`w` - show logged in users
