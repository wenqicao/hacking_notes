# NETWORK

* [Spoofr](https://github.com/d4rkcat/Spoofr) - ARP poison and sniff with DNS spoofing, urlsnarf, driftnet, ferret, dsniff, sslstrip and tcpdump  
* [ProxyChains](http://proxychains.sourceforge.net/) - TCP and DNS through proxy server. HTTP and SOCKS
* arpspoof
* [Ettercap](http://ettercap.github.io/ettercap/) - suite for man in the middle attacks
* netdiscover
* [Yersinia](http://www.yersinia.net/) - network tool designed to take advantage of weaknesses in different network protocols

DNS Cache Snooping
------------------

`nmap -sU -p 53 --script dns-cache-snoop.nse 8.8.8.8`

Other
-----

MAC address spoof: `ifconfig eth0 hw ether 00:11:22:33:44:55`
