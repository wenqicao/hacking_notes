# MISC

General wordlists: [SecLists](https://github.com/danielmiessler/SecLists)

GIT
---
```
git add .
git status
git commit -m "Commit Message"
git push -u alias master
Update repo: git pull [options] [<repository> [<refspec>…​]]
```

MARKDOWN
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

OSI Model
---------

1. Physical (cables, hubs)
2. Data Link (frames)
3. Network (packets)
4. Transport (TCP)
5. Session (logical ports)
6. Presentation (ASCII)
7. Application (SMTP)

Bug Bounties
------------

* [ExploitHub](https://exploithub.com/) - non 0-day exploit marketplace


Still to-do:
------------

p0wn pr0xy sqlmap  
Hash length extension attack (http://sakurity.com/lengthextension)
