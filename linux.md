LINUX

GENERAL
-------

If ifconfig is not found, try this: /sbin/ifconfig
File permissions: owner:group:world x=1 w=2 r=4


User Management
---------------

Add root user:

useradd -ou 0 -g 0 john
passwd john

Switch user: su

Chagne user password non-interactively:

echo "student:studying"|chpasswd

Add another non-root Kali user:

root@kali:~# useradd -m muts -G sudo -s /bin/bash
root@kali:~# passwd muts
Enter new UNIX password:
Retype new UNIX password:
passwd: password updated successfully


NETWORKING
----------

Find open ports:

netstat --listen
lsof -i

Open ports and established TCP connections: netstat -vatn
Only open UDP ports: netstat -vaun
FQDN: netstat -vat

Display all open IPv4 network files in use by the processes whose PID is 9255:

lsof -i 4 -a -p 9255