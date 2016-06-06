# MISC

General wordlists: [SecLists](https://github.com/danielmiessler/SecLists)

Git
---
```
git add .
git status
git commit -m "Commit Message"
git push -u alias master
Update repo: git pull [options] [<repository> [<refspec>…​]]
```

Markdown
--------

Line break: end line with two or more spaces.  

* [Markdown Cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)

Nessus
------

Admin panel is usually reachable at https://localhost:8834/

Reset admin panel password on Kali:

```sh
cd /opt/nessus/sbin
./nessuscli lsuser
./nessuscli chpasswd [username]
```

New PC Security Checklist
-------------------------

* Disable Flash in browser (`chrome://plugins`)
* Disable Java in browser (Start -> Configure Java -> Security -> Uncheck "Enable Java content in the browser")
* If Chrome, disable other things (omnibox leak etc.)
* Disable NetBIOS over TCP/IP (network settings)

TCP/IP
======

OSI Model
---------

1. Physical (cables, hubs); PDU: bit
2. Data Link (frames); PDU: frame
3. Network (packets); PDU: packet
4. Transport (TCP); PDU: segment (TCP), datagram (UDP)
5. Session (logical ports); PDU (5-7 layers): data (clear text, encrypted, compressed)
6. Presentation (ASCII)
7. Application (SMTP)

TCP Flags
---------

* CWR – Congestion Window Reduced (CWR) flag is set by the sending host to indicate that it received a TCP segment with the ECE flag set (added to header by RFC 3168).
* ECE (ECN-Echo) – indicate that the TCP peer is ECN capable during 3-way handshake (added to header by RFC 3168).
* URG – indicates that the URGent pointer field is significant
* ACK – indicates that the ACKnowledgment field is significant (Sometimes abbreviated by tcpdump as ".")
* PSH – Push function
* RST – Reset the connection (Seen on rejected connections)
* SYN – Synchronize sequence numbers (Seen on new connections)
* FIN – No more data from sender (Seen after a connection is closed)

Bug Bounties
------------

* [ExploitHub](https://exploithub.com/) - non 0-day exploit marketplace

Setting up TOR
--------------




Still to-do:
------------

p0wn pr0xy sqlmap  
Hash length extension attack (http://sakurity.com/lengthextension)
