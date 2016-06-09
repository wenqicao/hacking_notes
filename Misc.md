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

Bug Bounties
------------

* [ExploitHub](https://exploithub.com/) - non 0-day exploit marketplace

Setting up TOR
--------------

Country = Spain:  
```
apt-get install tor
echo ExitNodes {es} >> /etc/tor/torrc
service tor start
proxychains firefox
```
And set Firefox to use `127.0.0.1:9050` proxy.
