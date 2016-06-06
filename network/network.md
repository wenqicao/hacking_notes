# NETWORK

* [Spoofr](https://github.com/d4rkcat/Spoofr) - ARP poison and sniff with DNS spoofing, urlsnarf, driftnet, ferret, dsniff, sslstrip and tcpdump  
* [ProxyChains](http://proxychains.sourceforge.net/) - TCP and DNS through proxy server. HTTP and SOCKS
* arpspoof
* [Ettercap](http://ettercap.github.io/ettercap/) - suite for man in the middle attacks
* netdiscover
* [Yersinia](http://www.yersinia.net/) - network tool designed to take advantage of weaknesses in different network protocols
* [iodine](https://github.com/yarrick/iodine) - tunnel IPv4 data through a DNS server
* [dnscat2](https://github.com/iagox86/dnscat2) - encrypted C&C over DNS

DNS Cache Snooping
------------------

`nmap -sU -p 53 --script dns-cache-snoop.nse 8.8.8.8`

Wireshark
---------

Filters:
```
tcp.port==25
tcp.srcport!=53
tcp.dstport==80
ip.addr == 10.0.0.1
ip.addr != 10.0.0.1
ip.src==192.168.0.0/16
!udp
smb || dns || icmp
```

Other
-----

MAC address spoof: `ifconfig eth0 hw ether 00:11:22:33:44:55`  
View routing tables: `netstat -rn`
